# nginx-2420

INSTALL NEEDED SOFTWARE

1.To begin, install Vim by using ```sudo pacman -Syu Vim```, which is the text editor we will use to write and edit files. ```pacman``` is the package manager for linux and ```-Syu``` ensures that we have the latest package info before installing Vim.

2. Next, install Nginx using ```sudo pacman -S nginx```. Nginx is the package we will be using to host our webserver.

SETTING UP OUR DIRECTORY

1. create the root directory for the project, in this case we will be using
   web/html/nginx-2420
   
   ```mkdir -p /web/html/nginx-2420```

CREATING OUR HTML FILE

3. Copy and paste or write the following document into a file called index.html in our ./nginx-2420 directory.
   
   ```sudo vim index.html```
   
   ```<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>2420</title>
    <style>
        * {
            color: #db4b4b;
            background: #16161e;
        }
        body {
            display: flex;
            align-items: center;
            justify-content: center;
            height: 100vh;
            margin: 0;
        }
        h1 {
            text-align: center;
            font-family: sans-serif;
        }
    </style>
</head>
<body>
    <h1>All your base are belong to us</h1>
</body>
</html>```

CONFIGURING OUR NGINX SERVER BLOCK

1. Creating server blocks allow us to easily enable and disable different sites, so we will be creating one for our server.

2. To create our server block, we will create a directory named ```sites-available``` inside our /etc/nginx/ directory.
   ```cd /etc/nginx/```
   ```sudo mkdir sites-available```

3. Within our ./sites-available directory create a new file named ```nginx-2420```
   ```sudo vim nginx-2420```

4. Copy and paste the following configuration, replacing each line as desired.
   ```server {
         listen 80;
         server_name locahost;

         location / {
                     root /web/html/nginx-2420;
                     index index.html;
         }
   }```
   

