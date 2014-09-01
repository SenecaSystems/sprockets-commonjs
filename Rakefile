require 'bundler/gem_tasks'
require 'sprockets'
require 'sprockets/commonjs'
require 'rake/testtask'
require 'appraisal'

task :example do
  example_dir = File.expand_path('..', __FILE__)
  env         = Sprockets::Environment.new(example_dir)
  env.append_path 'examples/'
  Sprockets::CommonJS.module_paths += [File.join(example_dir, 'examples') ]

  target = File.expand_path('../examples/example.js', __FILE__)
  env['application.js'].write_to target
end


task :default => :test

Rake::TestTask.new do |t|
  t.test_files = FileList['test/**/*_test.rb']
  t.libs << 'lib' << 'test'
  t.warning = true
end
