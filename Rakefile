
files = %w[cf-install-virtualbox-20130626.box ci_with_warden_prereqs-20130626.box]
symlinks = %w[cf-install-virtualbox.box ci_with_warden_prereqs.box]

target_dir = "~/boxes"

desc "Create symlinks in #{target_dir} to Cloud Foundry Vagrant Boxes"
task :create_box_symlinks

[files, symlinks].transpose.each do |file, symlink|
  original_file = File.expand_path("../#{file}", __FILE__)
  boxes_symlink = File.expand_path("#{target_dir}/#{symlink}")
  
  file boxes_symlink, original_file do |t|
    sh "test -h #{boxes_symlink} && rm -f #{boxes_symlink}; true"
    sh "test -f #{boxes_symlink} && mv #{boxes_symlink} #{boxes_symlink}.orig; true"
    sh "ln -s '#{original_file}' '#{boxes_symlink}'"
  end

  task :create_box_symlinks => boxes_symlink
end

task :default => :create_box_symlinks