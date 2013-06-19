require 'rubygems'
require 'active_record'
require 'yaml'
require 'logger'
#require 'ruby-debug'

desc 'Load the environment'
task :environment do
  #debugger
  env = ENV['SINATRA_ENV'] || 'development'
  databases = YAML.load_file('config/database.yml')
  ActiveRecord::Base.establish_connection(databases[env])
end

namespace :db do
  desc 'Migrate the database'
  task(:migrate => :environment) do
    ActiveRecord::Base.logger = Logger.new(STDOUT)
    ActiveRecord::Migration.verbose = true
    ActiveRecord::Migrator.migrate('db/migrate')
  end
end

desc 'Run the test specs for the client'
task :test_client do
  sh "bundle exec rspec spec/client_spec.rb"
end

desc 'run server'
task 'run' do
  sh "bundle exec ruby service.rb -p 3000 -e test"
end
