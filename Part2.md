GETTING THE BACKEND SETUP

1. We first need to get the provided "hello-server" file onto our local linux machine. Assuming you've already
connected to a linux droplet, download the "hello-server" file, then connect to sftp using

```sftp -i do-key usr@dropletip```

2. With sftp, use ```put``` combined with the directory to your "hello-server" file to 
move it into your linux server. 

```sftp> put path/to/directory/hello-server```

3. with the file in your linux droplet use 


```sudo mv ~/hello-server /usr/local/bin/``` to move it to the directory.

Next, we need to make the file executable, use 

```sudo chmod +x /usr/local/bin/hello-server```

CREATING THE SERVICE FILE

1. Next we need to create the service file that allows us to run the backend. Use

```cd /etc/systemd/system/``` to move to the directory that we will create our service file. Next use

```sudo vim hello-server.service```

2. Within hello-server.service, we will set up our service file to allow us to access the hello-server file. 

```[Unit]
Description=Hello Server Service
After=network.target

[Service]
WorkingDirectory=/usr/local/bin
ExecStart=/usr/local/bin/hello-server
Restart=always

[Install]
WantedBy=multi-user.target
```

3. Next we need to save our changes, use

```:wq``` in the file

```sudo systemctl daemon-reload``` to reload the changes made

4. Next we want to start our service. Use

```sudo systemctl enable --now hello-server```

NGINX CONFIGURATION 

1. To reverse proxy requests from http://dropletip/hey and http://dropletip/echo, 
we need to configure our previously made nginx file in ```/etc/nginx/sites-available```

```sudo vim /etc/nginx/sites-available/hello-server```

2.Within this file, post this configuration

```server {
    listen 80;
    listen [::]:80;
    server_name _;
    root /web/html/nginx-2420;
    location / {
        try_files $uri $uri/ =404;
        index index.html index.htm;

    }
     location /hey {
        proxy_pass http://127.0.0.1:8080/hey;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
                                                                             location /echo {
        proxy_pass http://127.0.0.1:8080/echo;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }                                                                   }
```

3. We define a proxy_pass for http:127.0.0.1:8080 for both "hey" and "echo" for the backend service.

4. Finally, use 

```sudo nginx -t``` to verify we have written our server block without error

```sudo systemctl reload nginx``` to save our changes

UFW SETUP

UFW is our simple firewall that we will setup and configure to allow our backend. 

```sudo pacman -Syu``` to make sure our packages are up to date

```sudo pacman -S ufw``` to install UFW.

1. First we need to allow some specific ports through our firewall

```sudo ufw allow 22 80``` these ports allow us to continue to SSH in as well as allow HTML

2. Enable the firewall 

```sudo ufw enable```

3. Ensure that you have configured the firewall correctly. 

```sudo ufw status verbose```

![image](https://github.com/Ckwasnik/nginx-2420/assets/148382824/97199be4-1f21-4b27-a669-1fdd5be1b80e)

My configuration is a little bit wonky, but it should show that 22 and 80 are allowed through.

TEST

1. If everything is done correctly, using any service to test should return a message, in this example I used postman

![image](https://github.com/Ckwasnik/nginx-2420/assets/148382824/1917a11c-bd1a-4125-8bae-fd7be62f08e1)








