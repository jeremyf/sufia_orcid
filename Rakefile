# Add your own tasks in files placed in lib/tasks ending in .rake,
# for example lib/tasks/capistrano.rake, and they will automatically be available to Rake.

require File.expand_path('../config/application', __FILE__)

SufiaOrcid::Application.load_tasks

desc 'Responsible for doing some of the bootstrapping of the application for you.'
task :bootstrap do
  Rake::Task['jetty:download'].invoke
  Rake::Task['jetty:unzip'].invoke
  Rake::Task['jetty:config'].invoke
  Rake::Task['db:create'].invoke
  Rake::Task['db:schema:load'].invoke
  Rake::Task['db:seed'].invoke
  source = File.expand_path('../config/application.yml.example', __FILE__)
  target = File.expand_path('../config/application.yml', __FILE__)
  FileUtils.cp(source, target)
end
