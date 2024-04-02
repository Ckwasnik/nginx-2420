# nginx-2420

INSTALL NEEDED SOFTWARE

1.To begin, install Vim by using ```sudo pacman -Syu Vim```, which is the text editor we will use to write and edit files. ```pacman``` is the package manager for linux and ```-Syu``` ensures that we have the latest package info before installing Vim.

2. Next, install Nginx using ```sudo pacman -S nginx```. Nginx is the package we will be using to host our webserver.

SETTING UP OUR DIRECTORY

1. create the root directory for the project, in this case we will be using
   web/html/nginx-2420
   
   ```mkdir -p /web/html/nginx-2420```

2. Copy and paste or write the following document into a file called index.html in our nginx-2420 directory. 
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
