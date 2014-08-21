# encoding: utf-8

require "json"

url_pow     = "theatre"
url_live    = "anitochtheatre.com"
github_repo = "antiochtheatre/antiochtheatre.github.io"

desc "Delete old website files to start fresh."
task :clean do
  puts "Starting fresh!"
  system "rm -rf public"
end

desc "Design, write, and edit live."
task :default do
  system "jekyll build -w"
end

desc "Build a clean, compressed copy of the site."
task :build do
  system "jekyll build"
  puts "Done! See it locally at http://#{url_pow}.dev, or live at http://#{url_live}."
end

desc "Builds a fresh copy of your site, then opens it."
task :view => [:build] do
  system "open http://#{url_pow}.dev"
end

namespace :view do
  desc "View your site live."
  task :live do
    system "open http://#{url_live}"
  end

  desc "Generate an xip.io friendly URL."
  task :xip do
    ip = `ifconfig | grep 'inet ' | grep -v '127.0.0.1' | awk '{print $2}' | awk '{ printf "%s", $0 }'`
    url = "http://#{url_pow}.#{ip}.xip.io/"
    puts "Opening #{url}…"
    system "open #{url}"
  end

  desc "View your project on GitHub."
  task :github do
    system "open http://github.com/#{github_repo}"
  end

  desc "A quick glimpse at your GitHub repo’s watchers, stars, and forks."
  namespace :github do
    task :stats do
      puts "Downloading GitHub repo data through their API…"
      json = `curl https://api.github.com/repos/#{github_repo}`
      repo = JSON.parse(json)
      puts ""
      puts "-------------------------------------------------------------------"
      puts ""
      puts "#{github_repo} has #{repo['subscribers_count']} watchers, #{repo['stargazers_count']} stars and #{repo['forks_count']} forks."
      puts ""
      puts "-------------------------------------------------------------------"
      puts ""
    end
  end
end
