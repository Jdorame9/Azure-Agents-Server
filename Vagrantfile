$script = <<-SCRIPT
sudo apt update
sudo apt upgrade -y
sudo apt-get update
sudo apt-get upgrade -y

sudo apt install openjdk-17-jdk openjdk-17-jre -y
export JAVA_HOME=/usr/lib/jvm/java-17-openjdk-amd64

mkdir cd
cd temp

wget https://dlcdn.apache.org/maven/maven-3/3.8.8/binaries/apache-maven-3.8.8-bin.tar.gz
sudo tar xzf apache-maven-3.8.8-bin.tar.gz -C /usr/local
cd /usr/local
sudo mv /usr/local/apache-maven-3.8.8 /usr/local/maven
export MAVEN_HOME=/usr/local/maven
export PATH=$PATH:$MAVEN_HOME/bin

cd /home/vagrant
sudo rm -r temp

echo $JAVA_HOME
echo $MAVEN_HOME
SCRIPT

Vagrant.configure("2") do |config|
  config.vm.box = "hashicorp/bionic64"
  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  config.vm.network "private_network", ip: "10.20.19.95"
  config.vm.synced_folder "./agents-build","/home/vagrant/agents-build"
  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  config.vm.provider "virtualbox" do |vb|
    vb.name= "server-agents-build"
    vb.memory = "1024"
  end
  # Enable provisioning with a shell script. Additional provisioners such as
  # Ansible, Chef, Docker, Puppet and Salt are also available. Please see the
  # documentation for more information about their specific syntax and use.
  config.vm.provision :shell, :inline => $script
  #   apt-get update
  #   apt-get install -y apache2
  # SHELL
end
