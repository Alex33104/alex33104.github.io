# Setup Log (OCI Web Presence)

## Instance
- Oracle Linux (Always Free), public IP: 129.153.237.29

## System Prep
- Swap: fallocate -l 8G /swapfile; chmod 600; mkswap; swapon; /etc/fstab entry
- Packages: sudo dnf -y install git nodejs

## App
- mkdir ~/site && cd ~/site
- npm init -y
- npm install express
- index.html + index.js created (serve "/" and "/echo")

## Network
- firewalld: sudo firewall-cmd --add-port=3000/tcp --permanent && sudo firewall-cmd --reload
- OCI Security List/NSG: ingress TCP 3000 from 0.0.0.0/0

## Service
- /etc/systemd/system/echoapp.service with ExecStart=/usr/bin/node /home/opc/site/index.js
- sudo systemctl enable --now echoapp

## Tests
- On instance: curl -I http://127.0.0.1:3000/
- External: curl -I http://129.153.237.239:3000/
- /echo GET & POST verified

## GitHub Pages
- Repo: alex33104.github.io
- index.html meta-refresh to http://<IP>:3000
- Settings → Pages → Deploy from branch (main)
