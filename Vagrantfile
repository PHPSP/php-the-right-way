Vagrant.configure("2") do |config|
    config.vm.box = "precise32"
    config.vm.box_url = "http://files.vagrantup.com/precise32.box"
    config.vm.network :forwarded_port, guest: 4000, host: 4000

    $script = <<SCRIPT

echo "deb http://ftp.br.debian.org/debian wheezy main contrib non-free" > /etc/apt/sources.list

sudo -i
apt-get update

apt-get install ruby1.9.3 debian-archive-keyring make --yes --force-yes

# Baixando NodeJS e descompactando
cd /opt

wget -q http://nodejs.org/dist/v0.10.33/node-v0.10.33-linux-x86.tar.gz
tar -xsf node-v0.10.33-linux-x86.tar.gz

cd /usr/bin

# Criando links simbolicos, para que se utilize o Node posteriormente
ln -s /opt/node-v0.10.33-linux-x86/bin/node node
ln -s /opt/node-v0.10.33-linux-x86/bin/npm npm

# Instalando jekyll e rdiscount

gem install jekyll rdiscount --no-rdoc --no-ri

SCRIPT
    config.vm.provision :shell, :inline => $script
end