require 'bundler/setup'
require 'rspec/core/rake_task'
require 'rubocop/rake_task'
require 'foodcritic'
require 'kitchen'

task default: [:list]

desc 'Lists all the tasks.'
task :list do
  puts "Tasks: \n- #{(Rake::Task.tasks).join("\n- ")}"
end

desc 'Make sure we haev all our dependencies cleared'
task :check do
  sh 'bundle install'
  sh 'bundle exec berks install'
end

desc 'Builds the package.'
task :build do
  Rake::Task[:foodcritic].execute
  Rake::Task[:chefspec].execute
  Rake::Task[:rubocop].execute
end

desc 'Runs knife cookbook test against all the cookbooks.'
task :knife_test do
  sh 'bundle exec knife cookbook test -a'
end

desc 'Runs chefspec on the cookbook.'
task :chefspec do
  sh 'bundle exec rspec'
end

desc 'Runs foodcritic against the cookbook.'
task :foodcritic do
  sh 'bundle exec foodcritic -f any --tags ~FC003 --tags ~FC015 --tags ~FC023 .'
end

desc 'Runs foodcritic against the cookbook.'
task :rubocop do
  sh 'bundle exec rubocop'
end

desc 'Starts Gaurd'
task :guard do
  sh 'bundle exec guard'
end
