# Add your own tasks in files placed in lib/tasks ending in .rake,
# for example lib/tasks/capistrano.rake, and they will automatically be available to Rake.

require File.expand_path('../config/application', __FILE__)

Rails.application.load_tasks
Knapsack.load_tasks if defined?(Knapsack)

namespace :failing_cucumber_specs do
  FAILING_SCENARIOS_FILENAME = 'failing_scenarios.txt'

  task :record do
    begin
      Rake::Task['knapsack:cucumber'].invoke("-f rerun --out #{FAILING_SCENARIOS_FILENAME}")
    rescue SystemExit => e
      puts "#{e.class}: #{e.message}"
      exit 0
    end
  end

  task :rerun do
    unless File.zero?("#{FAILING_SCENARIOS_FILENAME}")
      exec("bundle exec cucumber @#{FAILING_SCENARIOS_FILENAME}")
    end
  end
end
