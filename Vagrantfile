unless Vagrant.has_plugin?("vagrant-docker-compose")
  system("vagrant plugin install vagrant-docker-compose")
  puts "Dependencies installed, please try the command again."
  exit
end

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/bionic64"

  port = 4000

  config.vm.network(:forwarded_port, guest: 4000, host: 8080)
  config.vm.network(:forwarded_port, guest: 9200, host: 9200)
  config.vm.network(:forwarded_port, guest: 9300, host: 9300)
  config.vm.network(:forwarded_port, guest: 5601, host: 5601)
  config.vm.network(:forwarded_port, guest: 6379, host: 6379)
  config.vm.network(:forwarded_port, guest: 5432, host: 5432)
  config.vm.network(:forwarded_port, guest: 5672, host: 5672)
  config.vm.network(:forwarded_port, guest: 5671, host: 5671)
  config.vm.network(:forwarded_port, guest: 27017, host: 27017)

  config.vm.provision :shell, inline: "apt-get update"
  config.vm.provision :docker
  config.vm.provision :shell, inline: "docker network create backend"
  config.vm.provision :docker_compose, yml: ["/vagrant/docker-compose.yml"], rebuild: true, project_name: "web-services", run: "always"
end