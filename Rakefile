desc 'Serve the Jekyll page locally'
task :serve do
  sh "jekyll serve"
end

desc 'Creates a new post skeleton'
task :post do
  require "Date"
  title = ENV['title']
  file_name = "#{Date.today}-#{title.downcase.gsub(/[^\w]+/, '-')}"

  file = File.join(
    File.dirname(__FILE__), '_posts',
    file_name + '.markdown'
  )

  File.open(file, "w") do |f|
    f << <<-EOS.gsub(/^    /, '')
    ---
    layout: post
    title: #{title}
    published: false
    categories:
    -
    ---

    EOS
  end

  `git add "#{file}"`
end

desc 'Updates the date for a specified blogpost'
task :update do
  require "Date"
  title = ENV['title'].downcase.gsub(/[^\w]+/, '-')

  old_post = File.join(
    File.dirname(__FILE__), '_posts',
    "*-#{title}" + '.markdown'
  )

  new_post = File.join(
    File.dirname(__FILE__), '_posts',
    "#{Date.today}-#{title}" + '.markdown'
  )

  File.rename Dir.glob(old_post).first, new_post
end
