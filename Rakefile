
symlinks = %w[cf-install-virtualbox.box ci_with_warden_prereqs.box]
target_dir = "~/boxes"

desc "Create symlinks in #{target_dir} to Cloud Foundry Vagrant Boxes"
task :create_box_symlinks

symlinks.each do |symlink|
  original_symlink = File.expand_path("../#{symlink}", __FILE__)
  boxes_symlink = File.expand_path("#{target_dir}/#{symlink}")
  
  file boxes_symlink, original_symlink do |t|
    sh "test -h #{boxes_symlink} && rm -f #{boxes_symlink}; true"
    sh "test -f #{boxes_symlink} && mv #{boxes_symlink} #{boxes_symlink}.orig; true"
    sh "ln -s '#{original_symlink}' '#{boxes_symlink}'"
  end

  task :create_box_symlinks => boxes_symlink
end

task :default => :create_box_symlinks