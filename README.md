# Aruba-Janus
My public Janus gateway hosted on Aruba

### Create a new Aruba Virtual Private Server (optional)

I chose the following (minimal and cheap) configuration. 

[![](https://github.com/guido57/Aruba-Janus/blob/master/screenshots/Ubuntu%20Server.JPG | width=100)]


### Install the necessary packages

1. Janus Gateway 
```
sudo snap install janus-gateway
```
2. Nginx Web Server. For details see: [How To Install Nginx on Ubuntu 18.04 [Quickstart]](https://www.digitalocean.com/community/tutorials/how-to-install-nginx-on-ubuntu-18-04-quickstart)
```
sudo apt install nginx
```
### Configure Nginx
1. Open the ufw firewall on ports 80 and 443
```
sudo ufw allow 'Nginx Full'
```
2. Check nginx browsing http://your_server_ip. You should see this: 
[![](https://github.com/guido57/Aruba-Janus/blob/master/screenshots/nginx.jpg)](https://github.com/guido57/Aruba-Janus/blob/master/screenshots/nginx.jpg)

3. Modify Nginx configuration on /etc/nginx/sites-available/default to make it similar to [/etc/nginx/sites-available/default](https://github.com/guido57/Aruba-Janus/blob/master/etc/nginx/sites-available/default)

### Configure Janus

1. Create a new systemd service file to start janus on boot: Copy janus.service to /etc/systemd/system/

2. Start the janus service
```
sudo systemctl start janus
```

3. Check if janus service started correctly.
You should see something like this:
```
● janus.service - Janus WebRTC Server
   Loaded: loaded (/etc/systemd/system/janus.service; enabled; vendor preset: enabled)
   Active: active (running) since Thu 2020-01-02 12:18:28 CET; 5s ago
 Main PID: 1554 (janus)
    Tasks: 20 (limit: 1110)
   CGroup: /system.slice/janus.service
           └─1554 /opt/janus/bin/janus -o

Jan 02 12:18:28 ARU-254300 janus[1554]: [WARN] Admin/monitor HTTP webserver disabled
Jan 02 12:18:28 ARU-254300 janus[1554]: [WARN] Admin/monitor HTTPS webserver disabled
Jan 02 12:18:28 ARU-254300 janus[1554]: JANUS REST (HTTP/HTTPS) transport plugin initialized!
Jan 02 12:18:28 ARU-254300 janus[1554]: Loading transport plugin 'libjanus_pfunix.so'...
Jan 02 12:18:28 ARU-254300 janus[1554]: [WARN] Unix Sockets server disabled (Janus API)
Jan 02 12:18:28 ARU-254300 janus[1554]: [WARN] Unix Sockets server disabled (Admin API)
Jan 02 12:18:28 ARU-254300 janus[1554]: [WARN] No Unix Sockets server started, giving up...
Jan 02 12:18:28 ARU-254300 janus[1554]: [WARN] The 'janus.transport.pfunix' plugin could not be initialized
Jan 02 12:18:28 ARU-254300 janus[1554]: [gstreamer-sample] New video stream! (ssrc=3395707327, index 0)
Jan 02 12:18:28 ARU-254300 janus[1554]: [theta-rpi] New video stream! (ssrc=2703245438, index 0)
```
5. Now enable janus service, so that it will start automatically on boot
```
sudo systemctl enable janus
```

### Check if everything is working properly

[![](https://github.com/guido57/Aruba-Janus/blob/master/screenshots/janus%20main%20page.JPG)](https://github.com/guido57/Aruba-Janus/blob/master/screenshots/janus%20main%20page.JPG)
