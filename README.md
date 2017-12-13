# LetsEncrypt-on-Nginx

Short and simple way to secure your website.

### Install NGINX
If you've already installed nginx, you can skip this step.
`sudo apt-get install nginx;`

Next you will go into this folder
`cd /etc/nginx/sites-available/`

copy and paste this into the folder
``
server {
    listen 80;

    server_name CHANGETHISTOYOURDOMAINNAME.com;

    location / {
        proxy_pass http://127.0.0.1:ADDYOURPORTNUMBER;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
}
``
 
save `CTRL+O` `ENTER` `CTRL+X`
