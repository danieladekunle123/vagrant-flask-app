Vagrant.configure("2") do |config|
  config.vm.box = "archlinux/archlinux"

  # Forward port 5000 (Flask default) to host
  config.vm.network "forwarded_port", guest: 5000, host: 8080

  # Provision the VM with the required packages and Flask setup
  config.vm.provision "shell", inline: <<-SHELL
    sudo pacman -Syu --noconfirm git nano vim python python-virtualenv python-pip
    python -m venv /home/vagrant/flask_venv
    source /home/vagrant/flask_venv/bin/activate
    pip install Flask
  SHELL

  # Upload the hello.py file
  config.vm.provision "file", source: "hello.py", destination: "/home/vagrant/hello.py"

  # Run the Flask app automatically after provisioning
  config.vm.provision "shell", inline: <<-SHELL
    source /home/vagrant/flask_venv/bin/activate
    flask --app /home/vagrant/hello run --host=0.0.0.0
  SHELL
end
