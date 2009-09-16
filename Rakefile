# written by travis jeffery <travisjeffery@gmail.com>
# contributions by scrooloose <github:scrooloose>

require 'rake'
require 'find'
require 'pathname'

IGNORE = [/\.gitignore$/, /Rakefile$/]

files = `git ls-files`.split("\n")
files.reject! { |f| IGNORE.any? { |re| f.match(re) } }

desc 'Zip up the project files'
task :zip do
  zip_name = File.basename(File.dirname(__FILE__))
  zip_name.gsub!(/ /, '_')
  zip_name = "#{zip_name}.zip"

  if File.exist?(zip_name)
    abort("Zip file #{zip_name} already exists. Remove it first.")
  end

  puts "Creating zip file: #{zip_name}"
  system("zip #{zip_name} #{files.join(" ")}")
end

desc 'Install plugin and documentation'
task :install do
  vimfiles = if ENV['VIMFILES']
               ENV['VIMFILES']
             elsif RUBY_PLATFORM =~ /(win|w)32$/
               File.expand_path("~/vimfiles")
             else
               File.expand_path("~/.vim")
             end
<<<<<<< HEAD
  files.each do |file|
    target_file = File.join(vimfiles, file)
    FileUtils.mkdir_p File.dirname(target_file)
    FileUtils.cp file, target_file

    puts "Installed #{file} to #{target_file}"
=======
  target_dir = File.join(vimfiles, 'plugin', 'jslint')
  FileUtils.mkdir_p target_dir
  files.each do |file|
    FileUtils.cp file, target_dir
    puts "Installed #{file} to #{target_dir}/"
>>>>>>> 8bc0814058436e213d5f8ed60754129db317abf5
  end

end

desc 'Pulls from origin'
task :pull do
  puts "Updating local repo..."
  system("cd " << Dir.new(File.dirname(__FILE__)).path << " && git pull")
end

desc 'Calls pull task and then install task'
task :update => ['pull', 'install'] do
  puts "Update of vim script complete."
end

task :default => ['update']
