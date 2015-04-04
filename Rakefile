require 'rake'
require 'jenkins_api_client'

task :jenkins do
  job_name = ENV['JOB_NAME']

  if job_name.nil?
    abort 'Error: please set JOB_NAME environment variable'
  end

  # cap production deploy --hosts myserviceweb001
  ignore, env, task, target_type, target_name = job_name.split('.')
  command = "cap #{env} #{task} --#{target_type} #{target_name}"
  puts "executing: #{command}"
  system command
  exit $?.exitstatus
end

task :list_jobs do
  puts jenkins.job.list('.+')
end

task :copy_job do
  jenkins.job.copy(ENV['FROM'], ENV['TO'])
end

def jenkins
  @jenkins ||= JenkinsApi::Client.new(
     :server_ip => 'localhost',
     :server_port => 8080,
     :ssl => false,
     :jenkins_path => '/',
     :username => 'XXXXXXXX',
     :password => 'YYYYYYYY'
  )
end
