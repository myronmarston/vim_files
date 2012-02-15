desc "Install my Janus customized vim files"
task :install do
  current_dir = Dir.pwd
  Dir.chdir(File.expand_path("~#{ENV['USER']}")) do
    %w[ vimrc.before vimrc.after gvimrc.before gvimrc.after ].each do |file|
      local_file = File.join(current_dir, file)
      sh "ln -sf '#{local_file}' '.#{file}'"
    end
  end
end

task :default => :install
