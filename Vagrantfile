VAGRANTFILE_API_VERSION = "2"

cluster = {
  "admin-swarm" => { :ip => "10.211.56.10", :cpus => 1, :mem => 1024 },
  "jenkins-worker-1" => { :ip => "10.211.56.11", :cpus => 1, :mem => 1024 },
  "iam-swarm-mngr-1" => { :ip => "10.211.56.20", :cpus => 1, :mem => 3072 },
  "iam-swarm-wrkr-1" => { :ip => "10.211.56.21", :cpus => 1, :mem => 3072 }
}

Vagrant.configure(VAGRANTFILE_API_VERSION) do |cfg|
  cluster.each_with_index do |(hostname, info), index|
    cfg.vm.define hostname do |config|
      config.vm.box = "generic/centos7"
      config.vm.network :private_network, ip: "#{info[:ip]}"
      config.vm.hostname = hostname
      config.ssh.insert_key = false

      config.vm.provider "virtualbox" do |v|
        v.name = hostname
        v.memory = info[:mem]
        v.cpus = info[:cpus]
        v.customize ["modifyvm", :id, "--vrde", "off"]
      end

      config.vm.provider "parallels" do |v|
        v.name = hostname 
        v.memory = info[:mem]
        v.cpus = info[:cpus]
        v.customize ["set", :id, "--isolate-vm", "on"]
      end

      end

    end
  end
end
