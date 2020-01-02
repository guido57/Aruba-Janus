# Aruba-Janus
My public Janus gateway hosted on Aruba

### Create a new Aruba Virtual Private Server (optional)

If you don't hanve any, create one server on Aruba. I chose the following (minimal and cheap) configuration. 

[![](https://github.com/guido57/Aruba-Janus/blob/master/Ubuntu%20Server.JPG)](https://github.com/guido57/Aruba-Janus/blob/master/Ubuntu%20Server.JPG)


### Connect to your Aruba Server by SSH and install the necessary packages

1. Janus Gateway 
```
sudo snap install janus-gateway
```

2. Create a new systemd service file to start janus on boot: Copy janus.service to /etc/systemd/system/

