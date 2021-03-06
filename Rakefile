require 'rubygems'
require 'rake'

begin
  require 'jeweler'
  Jeweler::Tasks.new do |gem|
    gem.name = "rtimbl"
    gem.summary = "Ruby bindings for TiMBL machine learning library"
    gem.description = "rtimbl provides Ruby language bindings to the TiMBL machine learning library.  See the README for more information."
    gem.email = "markisisme@gmail.com"
    gem.homepage = "http://github.com/markisisme/rtimbl"
    gem.authors = ["Mark Shirley"]
    gem.require_paths = ["lib", "ext"]
    gem.files.exclude 'swig/'
    gem.extensions = ["ext/extconf.rb"]
    gem.has_rdoc = false
    # gem is a Gem::Specification... see http://www.rubygems.org/read/chapter/20 for additional settings
  end
  Jeweler::GemcutterTasks.new
rescue LoadError
  puts "Jeweler (or a dependency) not available. Install it with: sudo gem install jeweler"
end

task :default => [:copy_swig_file]

task :copy_swig_file do |t|
  # copy swig file
  cp 'swig/ruby_timbl_wrap.cxx', 'ext/'
end

require 'rake/testtask'
Rake::TestTask.new(:test) do |test|
  test.libs << 'lib' << 'test'
  test.pattern = 'test/**/*_test.rb'
  test.verbose = true
end

begin
  require 'rcov/rcovtask'
  Rcov::RcovTask.new do |test|
    test.libs << 'test'
    test.pattern = 'test/**/*_test.rb'
    test.verbose = true
  end
rescue LoadError
  task :rcov do
    abort "RCov is not available. In order to run rcov, you must: sudo gem install spicycode-rcov"
  end
end

require 'rake/rdoctask'
Rake::RDocTask.new do |rdoc|
  if File.exist?('VERSION.yml')
    config = YAML.load(File.read('VERSION.yml'))
    version = "#{config[:major]}.#{config[:minor]}.#{config[:patch]}"
  else
    version = ""
  end

  rdoc.rdoc_dir = 'rdoc'
  rdoc.title = "rtimbl #{version}"
  rdoc.rdoc_files.include('README*')
  rdoc.rdoc_files.include('lib/**/*.rb')
end

