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

      # do ansible provision after last box starts
      if index == boxes.size - 1
        box_config.vm.provision "ansible" do |ansible|
          ansible.compatibility_mode = "2.0"
          ansible.playbook = "site.yml"
          ansible.limit = "all"
          ansible.inventory_path = "inventory/local_vagrant"
          ansible.become = true
          ansible.galaxy_role_file = "roles/requirements.yml"
          ansible.galaxy_command = "ansible-galaxy install -f -r %{role_file}"
        end
      end
    end
  end
end