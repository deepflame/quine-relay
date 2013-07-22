# Troubleshooting
#
# Long "Waiting for VM to boot"?
# -> forcefully power off the VM in the VirtualBox GUI and run "vagrant up" again.
#
require_relative 'src/code-gen.rb'

Vagrant.configure("2") do |config|

  config.vm.box = "raring32"
  config.vm.box_url = "http://cloud-images.ubuntu.com/vagrant/raring/current/raring-server-cloudimg-i386-vagrant-disk1.box"

  config.vm.provision :shell, :inline => "
    echo 'golang-go golang-go/dashboard boolean true' > preseed.conf
    sudo debconf-set-selections preseed.conf 
  "

  apts = CodeGen::List.reverse.flat_map {|c| c.steps.map {|step| step.apt } }
  config.vm.provision :shell, :inline => "sudo apt-get install -y #{ (apts + ["tcc"]).compact.uniq.sort.join " " }"

end
