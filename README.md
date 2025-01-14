Thinkpad T480 setup for my daily use

1. install [Linux Mint](https://linuxmint.com) then update all incuded software to the latest version
```sh
sudo apt update
sudo apt upgrade -y
```
2. install vim (replace vi) to edit system configuration file
```sh
sudo apt install vim
```
3. change keyboard layout, switch `Home` button to `PgUp` button and `End` button to `PgDn` button to optimize my typing comfort
```sh
sudo vi /usr/share/X11/xkb/keycodes/evdev
```
```conf
// <HOME> = 110;
// <PGUP> = 112;
<HOME> = 112;
<PGUP> = 110;
<DELE> = 119;
// <END> = 115;
// <PGDN> = 117;
<END> = 117;
<PGDN> = 115;
```
4. install tlp to optimize laptop battery life
```sh
sudo apt update
sudo apt install tlp tlp-rdw acpi-call-dkms
sudo systemctl enable tlp
sudo systemctl start tlp
sudo vi /etc/tlp.d/tlp.conf
```
```conf
DEVICES_TO_DISABLE_ON_STARTUP="bluetooth"
DEVICES_TO_DISABLE_ON_BAT="bluetooth"
START_CHARGE_THRESH_BAT0=40
STOP_CHARGE_THRESH_BAT0=80
START_CHARGE_THRESH_BAT1=40
STOP_CHARGE_THRESH_BAT1=80
```
```sh
sudo tlp start
sudo tlp-stat
```
5. install [Orchis Theme](https://github.com/vinceliuice/Orchis-theme)
6. install chrome, telegram, etc
7. install [Sublime Text](https://sublimetext.com) and [Sublime Merge](https://sublimemerge.com)
```sh
wget -qO - https://download.sublimetext.com/sublimehq-pub.gpg | gpg --dearmor | sudo tee /etc/apt/trusted.gpg.d/sublimehq-archive.gpg > /dev/null
echo "deb https://download.sublimetext.com/ apt/stable/" | sudo tee /etc/apt/sources.list.d/sublime-text.list
sudo apt update
sudo apt install sublime-text sublime-merge
```
8. install go
```sh
sudo rm -rf /usr/local/go
mkdir -p $HOME/dev/deps/gopath
wget https://go.dev/dl/go1.23.4.linux-amd64.tar.gz
sudo tar -C /usr/local -xzf go1.23.4.linux-amd64.tar.gz
vi ~/.profile
```
```sh
export GOROOT=/usr/local/go
export GOPATH=$HOME/dev/deps/gopath
export PATH=$GOPATH/bin:$GOROOT/bin:$PATH
```
9. install nodejs
```sh
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.1/install.sh | bash
nvm install 22
node -v # should print `v22.12.0`
npm -v # should print `10.9.0`
```
10. install php
```sh
sudo add-apt-repository ppa:ondrej/php
sudo apt update
sudo apt install php8.4 ca-certificates apt-transport-https software-properties-common
php -v # should print `PHP 8.4.1`
```
11. install postgresql
12. install mariadb
```sh
curl -LsS https://r.mariadb.com/downloads/mariadb_repo_setup | sudo bash -s -- --os-type=ubuntu --os-version=noble
sudo apt update
sudo apt install mariadb-server mariadb-client mariadb-backup
```
13. install dbeaver
```
sudo  wget -O /usr/share/keyrings/dbeaver.gpg.key https://dbeaver.io/debs/dbeaver.gpg.key
echo "deb [signed-by=/usr/share/keyrings/dbeaver.gpg.key] https://dbeaver.io/debs/dbeaver-ce /" | sudo tee /etc/apt/sources.list.d/dbeaver.list
sudo apt update
sudo apt install dbeaver-ce
```
14. install docker
```sh
for pkg in docker.io docker-doc docker-compose docker-compose-v2 podman-docker containerd runc; do sudo apt-get remove $pkg; done
sudo apt update
sudo apt install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc
echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu noble stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt update
sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
sudo usermod -aG docker $USER
newgrp docker
```
15. Install postman
```sh
sudo rm -rf /opt/Postman
tar -C /tmp/ -xzf <(curl -L https://dl.pstmn.io/download/latest/linux64) && sudo mv /tmp/Postman /opt/
sudo tee -a /usr/share/applications/postman.desktop << END
[Desktop Entry]
Encoding=UTF-8
Name=Postman
Exec=/opt/Postman/Postman
Icon=/opt/Postman/app/resources/app/assets/icon.png
Terminal=false
Type=Application
Categories=Development;
END
```
