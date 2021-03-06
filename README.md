# DevOps Test

- Used vagrant(v2.0.0) to quickly spin up and create centos virtual machines
- Generated Self-Signed SSL Certificates with openssl
- Servers are setup using Ansible(v2.2.0)
- Centos7/Nginx/Firewalld

## vagrant-standalone-webserver
- Uses Nginx to host static website
- Site is available from port 443(HTTPS) and is also setup to redirect when port 80(HTTP) is accessed

## vagrant-lb-webservers
- 3 Nginx Web Servers host the same static site from port 80(HTTP)
- Load Balancer
  - Uses an Nginx Reverse Proxy to balance between the 3 web servers
  - Handles the Self-Signed SSL Certificate for all servers
  - Site is available from port 443(HTTPS) and is also setup to redirect when port 80(HTTP) is accessed

## vagrant-lb-with-docker
- 1 Nginx Web Server w/SSL & load balances docker containers(nginx - static sites)
- docker containers all share the same volume - ```-v /var/www/portfolio:/usr/share/nginx/html"```

## ansible-set-up-lbnginx-with-docker
## ansible-set-up-lbhaproxy-with-docker

## Use
- ```cd``` into folder and run ```vagrant up```
- ex. ```cd LoadBalancer && vagrant up```
- View site at: http://192.168.50.100
- Use ```destroyandrebuild``` to Stop and Rebuild VM to test out new changes

## Ansible Only for Remote Server Deployment
- vagrant up --no-provision
- Update ansible playbook files 'hosts' field. Change 'all' to reflect correct group name
- Standalone_WebServer: ```ansible-playbook -i hosts webserver.yml ```
- LoadBalanced_WebServer: ```ansible-playbook -i hosts loadbalancer.yml && ansible-playbook -i hosts webserver.yml ```
