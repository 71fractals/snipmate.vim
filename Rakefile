require 'rake'
require 'rake/contrib/sshpublisher'

# TODO: I will try to make it more DRY later  :P
files = ['after/plugin/snipMate.vim', 'autoload/snipMate.vim', 'doc/snipMate.txt', 'ftplugin/html_snip_helper.vim', 'plugin/snipMate.vim', 'snippets/_.snippets', 'snippets/autoit.snippets', 'snippets/c.snippets', 'snippets/cpp.snippets', 'snippets/erlang.snippets', 'snippets/html.snippets', 'snippets/java.snippets', 'snippets/javascript.snippets', 'snippets/mako.snippets', 'snippets/objc.snippets', 'snippets/perl.snippets', 'snippets/php.snippets', 'snippets/python.snippets', 'snippets/ruby.snippets', 'snippets/sh.snippets', 'snippets/snippet.snippets', 'snippets/tcl.snippets', 'snippets/tex.snippets', 'snippets/vim.snippets', 'snippets/zsh.snippets', 'syntax/snippet.vim']

# mix from vim-rails and nerdtree projects
desc "Install"
task :install do
  vimfiles = if ENV['VIMFILES']
               ENV['VIMFILES']
             elsif RUBY_PLATFORM =~ /(win|w)32$/
               File.expand_path("~/vimfiles")
             else
               File.expand_path("~/.vim")
             end

  puts "Installing..."
  files.each do |file|
    target_file = File.join(vimfiles, file)
    FileUtils.mkdir_p(File.dirname(target_file))
    FileUtils.cp(file, target_file)
    puts "  Copied #{file} to #{target_file}"
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

desc 'Uninstall plugin and documentation'
task :uninstall do
  vimfiles = if ENV['VIMFILES']
               ENV['VIMFILES']
             elsif RUBY_PLATFORM =~ /(win|w)32$/
               File.expand_path("~/vimfiles")
             else
               File.expand_path("~/.vim")
             end
  files.each do |file|
    target_file = File.join(vimfiles, file)
    FileUtils.rm target_file

    puts "Uninstalled #{target_file}"
  end

end

task :default => ['update']
