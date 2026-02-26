boxes = [
    {
      name: "srv1",
      box: "cloud-image/ubuntu-24.04",
      hostname: "srv1.local",
      memory: 2048,
      cpus: 2,
      ip: "192.168.56.111"
    },
    {
      name: "srv2",
      box: "cloud-image/ubuntu-24.04",
      hostname: "srv2.local",
      memory: 2048,
      cpus: 2,
      ip: "192.168.56.112"
    },
    {
      name: "srv3",
      box: "cloud-image/ubuntu-24.04",
      hostname: "srv3.local",
      memory: 2048,
      cpus: 2,
      ip: "192.168.56.113"
    }
  ]

Vagrant.require_version ">= 2.0.0"

Vagrant.configure("2") do |config|
  config.ssh.insert_key = false

  # Configure all VMs
  boxes.each_with_index do |box, index|
    config.vm.define box[:name] do |box_config|
      box_config.vm.box = box[:box]
      box_config.vm.hostname = box[:hostname]
      box_config.vm.network "private_network", ip: box[:ip]
    end
  end
end