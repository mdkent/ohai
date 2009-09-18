require 'rubygems'
require 'rake/gempackagetask'
require 'rubygems/specification'
require 'date'
require 'spec/rake/spectask'

NAME = "ohai"
VERSION = "0.3.3"
AUTHOR = "Adam Jacob"
EMAIL = "adam@opscode.com"
HOMEPAGE = "http://wiki.opscode.com/display/ohai"
SUMMARY = "Ohai profiles your system and emits JSON"
FILES = %w(LICENSE README.rdoc Rakefile) + Dir.glob("{extras,lib,spec}/**/*")

spec = Gem::Specification.new do |s|
  s.name = NAME 
  s.version = VERSION
  s.platform = Gem::Platform::RUBY
  s.has_rdoc = true
  s.summary = SUMMARY
  s.description = s.summary
  s.author = AUTHOR
  s.email = EMAIL
  s.homepage = HOMEPAGE
  
  s.add_dependency "json"
  s.add_dependency "extlib"
  s.add_dependency "systemu"
  s.bindir = "bin"
  s.executables = %w(ohai)
  
  s.require_path = 'lib'
  s.autorequire = NAME
  s.files = FILES
end

task :default => :spec

desc "Run specs"
Spec::Rake::SpecTask.new do |t|
  t.spec_files = FileList['spec/**/*_spec.rb']
  t.spec_opts = %w(-fs --color)
end


Rake::GemPackageTask.new(spec) do |pkg|
  pkg.gem_spec = spec
end

desc "install the gem locally"
task :install => [:package] do
  sh %{sudo gem install pkg/#{NAME}-#{VERSION}}
end

desc "create a gemspec file"
task :make_spec do
  File.open("#{NAME}.gemspec", "w") do |file|
    file.puts spec.to_ruby
  end
end

Rake::PackageTask.new(NAME, VERSION) do |pkg|
  pkg.need_tar_gz = true
  pkg.need_tar_bz2 = true
  pkg.package_files = FILES
end
