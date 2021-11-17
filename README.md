# Redmine Docker

Custom Redmine 4.2.3 docker based on bitnami image, with Subversion support and additional plugins:

https://github.com/Smile-SA/redmine_smile_togglesidebar  
https://github.com/anteo/redmine_custom_workflows  
https://github.com/jgraichen/redmine_dashboard  
https://github.com/jkraemer/stopwatch  
https://github.com/taqueci/redmine_local_avatars  

## Usage

Get Linux based host with docker support installed.  
For example, you can install minimum installation of Ubuntu 20.04 server and run:

```
sudo apt install docker docker-compose git
sudo usermod -aG docker (your account)
cd ~
git clone https://gitlab.rk86.com/alex/redmine-docker.git
cd redmine-docker
cp docker-compose.yml.defaul docker-compose.yml
# Adjust docker-compose.yml, at the very minimum set DB and Redmine admin passwords 
cd alex-redmine
./build
cd ..
./docker-redmine -start
```

After a few minutes, open browser to http://(your_ip)  
login with admin and password you specified in docker-compose.yml

The default volumes are located in /var/lib/docker/volumes/redmine*

"docker-redmine" - is a simple helper for start/stop/backup.

## Links
https://hub.docker.com/r/bitnami/redmine  
https://github.com/bitnami/bitnami-docker-redmine  
https://github.com/sameersbn/docker-redmine
