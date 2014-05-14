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
end

namespace :force_profile_states_to do
  desc 'For demo purposes only! Set all profiles states to :authenticated_connection'
  task :authenticated_connection => [:environment, :clean_slate] do
    User.all.each_with_index do |user, index|
      orcid_profile_id = sprintf("0000-0001-0234-%04d", index+1)
      access_token = sprintf('4a8e9a1a-e53a-448b-b81d-e541c347a%03d', index)
      refresh_token = sprintf('b39b89ce-92df-4d99-bd25-309a869d2%03d', index)
      Orcid::ProfileRequest.create!(
        user_id: user.id,
        given_names: 'Given',
        family_name: 'Family',
        primary_email: "user-#{index}@sufia.org",
        orcid_profile_id: orcid_profile_id
      )
      authentication = Orcid.connect_user_and_orcid_profile(user, orcid_profile_id)
      authentication.update(
        access_token: access_token,
        refresh_token: refresh_token
      )

      guard_state(:authenticated_connection, user)
    end
  end

  desc 'For demo purposes only! Set all profiles states to :pending_connection'
  task :pending_connection => [:environment, :clean_slate] do
    User.all.each_with_index do |user, index|
      orcid_profile_id = sprintf("0000-0001-0234-%04d", index+1)
      Orcid::ProfileRequest.create!(
        user_id: user.id,
        given_names: 'Given',
        family_name: 'Family',
        primary_email: "user-#{index}@sufia.org",
        orcid_profile_id: orcid_profile_id
      )
      Orcid.connect_user_and_orcid_profile(user, orcid_profile_id)

      guard_state(:pending_connection, user)
    end
  end

  desc 'For demo purposes only! Set all profiles states to :profile_request_pending'
  task :profile_request_pending => [:environment, :clean_slate] do
    User.all.each_with_index do |user, index|
      Orcid::ProfileRequest.create!(
        user_id: user.id,
        given_names: 'Given',
        family_name: 'Family',
        primary_email: "user-#{index}@sufia.org"
      )
      guard_state(:profile_request_pending, user)
    end
  end

  desc 'For demo purposes only! Set all profiles states to :unknown'
  task :unknown => [:environment, :clean_slate] do
    User.all.each_with_index do |user, index|
      guard_state(:unknown, user)
    end
  end

  task :clean_slate => [:environment] do
    Orcid::ProfileRequest.destroy_all
    Orcid.authentication_model.destroy_all

    def guard_state(expected, user)
      actual = Orcid::ProfileStatus.for(user)
      if expected != actual
        raise "Expected #{expected.inspect}, got #{actual.inspect}"
      end
    end

  end

end
