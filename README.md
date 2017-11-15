# DevOps Test

- Used vagrant to quickly spin up and create centos virtual machines
- Generated Self-Signed SSL Certificates with openssl
- Servers are setup using Ansible
- Nginx
- Firewalld

## Standalone Web Server
- Uses nginx to host static website
- Site is available from port 443(HTTPS) and is also setup to redirect when port 80(HTTP) is accessed

## Load Balanced Web Server
- 3 Nginx Web Servers host the same static site from port 80(HTTP)
- Load Balancer
  - Uses an Nginx Reverse Proxy to balance between the 3 web servers
  - Handles the Self-Signed SSL Certificate for all servers
  - Site is available from port 443(HTTPS) and is also setup to redirect when port 80(HTTP) is accessed

## Use
- ```cd``` into folder and run ```vagrant up```
- ex. ```cd LoadBalancer && vagrant up```
- View site at: http://192.168.50.100
- Use ```destroyandrebuild``` to Stop and Rebuild VM to test out new changes
