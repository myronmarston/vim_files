desc "Symlink vim files"
task :symlink do
  current_dir = Dir.pwd
  Dir.chdir(File.expand_path("~#{ENV['USER']}")) do
    %w[ vimrc.before vimrc.after gvimrc.before gvimrc.after ].each do |file|
      local_file = File.join(current_dir, file)
      sh "ln -sf '#{local_file}' '.#{file}'"
    end
  end
end

desc "Install my Janus customized vim files"
task :install_plugins do
  extra_plugins = %w[
    git://github.com/vim-scripts/bufexplorer.zip.git
    git://github.com/tpope/vim-rvm.git
  ]

  Dir.chdir(File.expand_path("~#{ENV['USER']}")) do
    FileUtils.mkdir_p('.janus')
    Dir.chdir('.janus') do
      extra_plugins.each do |plugin|
        dir = plugin.split('/').last.gsub(/.git$/, '')
        if File.exist?(dir)
          puts "Updating #{dir}..."
          Dir.chdir(dir) { sh "git pull --rebase" }
        else
          puts "Installing #{dir}..."
          sh "git clone #{plugin}"
        end
      end
    end
  end
end

desc "Install everything"
task :install_all => [:symlink, :install_plugins]

task :default => :install_all
