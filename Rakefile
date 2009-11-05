task :default => ["test"]
task :test do exec "bash -l -c \"./test/suite\"" ; end

namespace :gem do
  task :refresh do
    exec "gem uninstall rvm ; rm -f pkg/*.gem ./rvm.gemspec && rake gemspec && rake build && gem install pkg/*.gem --no-rdoc --no-ri"
  end

  desc "Build the rvm gem."
  task :build do
puts <<-LOCAL_INSTALL_WARNING

  $(tput setaf 3)INSTALLING FROM SOURCE$(tput sgr0)

  If you are using rvm from source, DO NOT build the gem.
  Instead, run the following from the rvm source's root dir.

    $(tput setaf 2)For installing/updating:  ./install$(tput sgr0)

LOCAL_INSTALL_WARNING
    puts "$(gem build rvm.gemspec)"
  end

  desc "Install the rvm gem (NO sudo)."
  task :install do
    %x{gem install rvm*.gem --no-rdoc --no-ri -l}
  end
end

begin
  require "jeweler"
  require "lib/rvm/version"

  Jeweler::Tasks.new do |gemspec|
    gemspec.name            = "rvm"
    gemspec.version         = RVM::Version::STRING
    gemspec.summary         = "Ruby Version Manager (rvm)"
    gemspec.require_paths   = ["lib"]
    gemspec.date            = Time.now.strftime("%Y-%m-%d")
    gemspec.description     = "Manages Ruby interpreter installations and switching between them."
    gemspec.platform        = Gem::Platform::RUBY
    gemspec.files           = ["install", "README", "LICENCE", "rvm.gemspec", "bash/*", "binscripts/*", "scripts/*", "examples/*", "config/*", Dir::glob("lib/**/**")].flatten
    gemspec.executables     = Dir::glob("bin/rvm-*").map{ |script| File::basename script }
    gemspec.require_path    = "lib"
    gemspec.has_rdoc        = File::exist?("doc")
    gemspec.rdoc_options    = ["--inline-source", "--charset=UTF-8"]
    gemspec.authors         = ["Wayne E. Seguin"]
    gemspec.email           = "wayneeseguin@gmail.com"
    gemspec.homepage        = "http://github.com/wayneeseguin/rvm"
    gemspec.extensions      << "extconf.rb" if File::exists?("extconf.rb")
    gemspec.rubyforge_project = "rvm"
  end
rescue LoadError
  puts "Jeweler not available. Install it with: gem install jeweler -s http://gemcutter.org/"
end

