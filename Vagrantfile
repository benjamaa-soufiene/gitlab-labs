# === 🦊 GitLab ===

BOX_IMAGE = "bento/ubuntu-16.04"
VERSION = "1.0"

# GitLab instance
GITLAB_DOMAIN = "gitlab-ce.test"
GITLAB_IP = "172.16.245.121"
GITLAB_PUB_IP = "192.168.1.121"
GITLAB_NAME = "gitlab"

=begin
On the host machine you need to update your `/etc/hosts` file with:

- the ip adress => `GITLAB_IP = "172.16.245.121"`
- the domain name of the GitLab instance

👋 this `GITLAB_PUB_IP = "192.168.1.121"` is used only if you want to reach the GitLab instance from another computer on your network

```shell
sudo pico /etc/hosts

# in the hosts file:
172.16.245.121 gitlab-ce.test

# Now, you can reach the instance like that http://gitlab-ce.test
```
=end

Vagrant.configure("2") do |config|
  config.vm.box = BOX_IMAGE

  ENV['LC_ALL']="en_US.UTF-8"

  config.vm.define "#{GITLAB_NAME}" do |node| 

    node.vm.hostname = "#{GITLAB_NAME}"
    
    # if you're host is a linux machine
    # node.vm.network "public_network", ip:"#{GITLAB_PUB_IP}",  bridge: "wlp58s0"
    # if you're host is a osx machine
    node.vm.network "public_network", ip:"#{GITLAB_PUB_IP}",  bridge: "en0: Wi-Fi (AirPort)"
    node.vm.network "private_network", ip: "#{GITLAB_IP}"

    node.vm.provider "virtualbox" do |vb|
      vb.memory = 4096
      vb.cpus = 2
      vb.name = "#{GITLAB_NAME}"
    end

    node.vm.provision :shell, inline: <<-SHELL
      echo "👋 setup"

      # download GitLab CE packages
      curl -s https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.deb.sh | sudo bash
      
      
      # download GitLab EE packages
      # curl -s https://packages.gitlab.com/install/repositories/gitlab/gitlab-ee/script.deb.sh | sudo bash      
      
      # install GitLab CE
      EXTERNAL_URL="http://#{GITLAB_DOMAIN}" apt-get install -y gitlab-ce
      # install GitLab EE
      # EXTERNAL_URL="http://#{GITLAB_DOMAIN}" apt-get install -y gitlab-ee

      echo "👋 Bye! go to http://#{GITLAB_DOMAIN}"
      echo " - Go to http://#{GITLAB_DOMAIN}"
      echo " - Change the password of the root user"
      echo "Enjoy ❤️ Devops with 🦊 GitLab"

    SHELL
    
  end
  # end of GitLab setup

end
