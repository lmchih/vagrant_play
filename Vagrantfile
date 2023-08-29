Vagrant.configure("2") do |config|
    config.vm.box = "starboard/ubuntu-arm64-20.04.5"
    config.vm.box_version = "20221120.20.40.0"
    config.vm.box_download_insecure = true
    
    # require plugin https://github.com/leighmcculloch/vagrant-docker-compose
    config.vagrant.plugins = "vagrant-docker-compose"

    # install docker and docker-compose
    config.vm.provision :docker
   
    # TODO: install nginx
 
    config.vm.provider "vmware_desktop" do |v|
        v.ssh_info_public = true
        v.gui = true
        v.linked_clone = false
        v.vmx["ethernet0.virtualdev"] = "vmxnet3"
     end
    
    config.vm.provision "shell", inline: <<-SHELL
      apt-get update
      apt-get install -y graphite-web
      apt-get install -y net-tools

      docker pull nginx
      docker run -idt --name nginx -p 80:80 nginx
     SHELL
end
