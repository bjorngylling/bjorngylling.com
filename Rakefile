task :default => 'serve'

desc 'Serve the Jekyll page locally'
task :serve do
  sh "jekyll serve"
end

desc 'Creates a new post skeleton'
task :post, [:title] do |t, args|
  require "Date"
  file_name = "#{Date.today}-#{args.title.downcase.gsub(/[^\w]+/, '-')}"

  file = File.join(
    File.dirname(__FILE__), '_posts',
    file_name + '.markdown'
  )

  File.open(file, "w") do |f|
    f << <<-EOS.gsub(/^    /, '')
    ---
    layout: post
    title: #{args.title}
    published: false
    categories:
    -
    ---

    EOS
  end

  `git add "#{file}"`
end

desc 'Updates the date for a specified blogpost'
task :update, [:title] do |t, args|
  require "Date"
  title = args.title.downcase.gsub(/[^\w]+/, '-')

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
