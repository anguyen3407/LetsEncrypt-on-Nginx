# LetsEncrypt-on-Nginx

Short, simple and free way to secure your website.

## Install NGINX
If you've already installed nginx, you can skip this step.

`sudo apt-get install nginx;`

Next you will go into this folder

`cd /etc/nginx/sites-available/`

copy and paste this into the folder


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


 
save [CTRL+O] [enter] [CTRL+X]

## Let's Encrypt

Go to this website
`https://letsencrypt.org/getting-started/`

Scroll down to the "With Shell Access" paragraph and click on the blue `Certbot` link.
Choose your software `nginx` and system `Ubuntu 16.04`

### Install 

Open up your terminal 

    ssh root@YOURDOMAINNAME.com

    ** enter your password

On Ubuntu systems, the Certbot team maintains a PPA. Once you add it to your list of repositories all you'll need to do is apt-get the following packages.

    $ sudo apt-get update
    $ sudo apt-get install software-properties-common
    $ sudo add-apt-repository ppa:certbot/certbot
        ** press [enter] to accept and continue
    $ sudo apt-get update
    $ sudo apt-get install python-certbot-nginx 
        ** enter your email address
    
 ### Get Started
 Certbot has an Nginx plugin, which is supported on many platforms, and automates both obtaining and installing certs:
 
    $ sudo certbot --nginx
        ** Select name you would like to activate HTTPS for
    
Running this command will get a certificate for you and have Certbot edit your Nginx configuration automatically to serve it. If you're feeling more conservative and would like to make the changes to your Nginx configuration by hand, you can use the certonly subcommand:
    
    $ sudo certbot --nginx certonly
        ** Select the appropriate number [1-2] then [enter] (press 'c' to cancel):
            ** Select [2] and then [enter]
       
#### Congratulations! Your https is activated! Now proceed to the next step to renew your certificate automatically.
    
 ### Automating renewal
The Certbot packages on your system come with a cron job that will renew your certificates automatically before they expire. Since Let's Encrypt certificates last for 90 days, it's highly advisable to take advantage of this feature. You can test automatic renewal for your certificates by running this command:

    $ sudo certbot renew --dry-run
    
If that appears to be working correctly, you can arrange for automatic renewal by adding a cron or systemd job which runs the following:
 
    certbot renew 

To learn more about renewing, follow this link https://certbot.eff.org/docs/using.html#renewal

# Troubleshooting
Some reasons your https is still not activating

1. You didn't install nginx. If you aren't sure whether you installed it or not, install it again. It will not affect anything. 

2. Your proxy_pass is incorrect
** Open up your terminal

`cd /etc/nginx/sites-available/`

** Copy and replace the proxy_pass below and insert your port number

            proxy_pass http://127.0.0.1:ADDYOURPORTNUMBER;
            
save [CTRL+O] [enter] [CTRL+X]

3. You entered the wrong port number


###### https://github.com/anguyen3407/Hosting-React-Digital-Ocean
###### https://letsencrypt.org/getting-started/
###### https://certbot.eff.org/
###### https://certbot.eff.org/#ubuntuxenial-nginx
