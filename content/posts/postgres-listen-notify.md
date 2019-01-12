+++ 
date = "2011-04-13"
title = "Postgres LISTEN / NOTIFY with Node.js"
slug = "postgres-listen-notify"
tags = ["Postgres", "Node.js", "LISTEN / NOTIFY"]
categories = []
+++

I'm sure most of you have been hearing about [Node.js](http://nodejs.org) lately, it has been
causing quite a buzz. If you're wondering what Node.js is all about I
recommend you watch one of [Ryan Dahls](https://twitter.com/#!/ryah) [presentations](http://camp.nodejs.org/videos/session-01_introduction_to_node-ryan_dahl.html "Most recent") [on](http://www.youtube.com/watch?v=jo_B4LTHi3I) [the](http://developer.yahoo.com/yui/theater/video.php?v=dahl-node) [subject](http://jsconf.eu/2009/video_nodejs_by_ryan_dahl.html).

# Postgres
Interestingly [Postgres](http://www.postgresql.org) has a feature that goes very well with the
asynchronously nature of Node.js. The Postgres commands LISTEN and
NOTIFY along with triggers you can have NOTIFY events fire when certain
queries are performed on specific tables.

I wrote a short Node.js script that basically "watches" a table in a
Postgres database. Say we have the following table:
{{< highlight sql >}}
CREATE TABLE foo (id serial primary key, name varchar);
{{< / highlight >}}
We then create a function which will perform the notification to a
channel we can later watch in our Node.js application.

{{< highlight sql >}}
CREATE FUNCTION notify_trigger() RETURNS trigger AS $$
DECLARE
BEGIN
  PERFORM pg_notify('watchers', TG_TABLE_NAME || ',id,' || NEW.id );
  RETURN new;
END;
$$ LANGUAGE plpgsql;
{{< / highlight >}}
The interesting line here is the call to `pg_notify`, the
arguments here are the channel name to send the notification to and the
second part is the message. In this case the message consists of a
comma-separated string including the table name that the
notification came from (in our case this will be `bar`) and then the id of the
record. `NEW` is the record that fired the trigger so we could use
`NEW.name` here as well to get the value of the column `name`. The
channel-name can also consist of variables. For example if we had 
`pg_notify('watch_' || lower(NEW.name), 'id,' || NEW.id)` and inserted a
new record with the column `name` set to `bar` it would notify
the channel `watch_bar` with the message `id,X` where `X` is the new
records id. This could be used to listen for insertions where some
column has a specific value. It is worth noting that the message part in
notifications was introduced in Postgres 9.x, 8.x will only support
notifying a channel without passing any message.

Some of you might have noticed that we need to do one more thing in
Postgres to get this to work. We need to set up a trigger to fire this
newly created function when a insert-query is performed on our table.
{{< highlight sql >}}
CREATE TRIGGER watched_table_trigger AFTER INSERT ON foo
FOR EACH ROW EXECUTE PROCEDURE notify_trigger();
{{< / highlight >}}

# Node.js
To interact with Postgres from Node.js I use the excellent module
[node-postgres](https://github.com/brianc/node-postgres) by [Brian
Carlson](https://twitter.com/briancarlson).
{{< highlight js >}}
var pg = require ('pg');

var pgConString = "postgres://localhost/bjorngylling"

pg.connect(pgConString, function(err, client) {
  if(err) {
    console.log(err);
  }
  client.on('notification', function(msg) {
    console.log(msg);
  });
  var query = client.query("LISTEN watchers");
});
{{< / highlight >}}
This will set up the postgres-client to listen on the `watchers` channel
and when a notification comes in it will just print it to the console.
If you are trying this on your own machine you will probably have to
change your `pgConString` to reflect your Postgres-setup.
