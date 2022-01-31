
# Created VM

# VM Setup

    sudo apt update
    sudo apt upgrade
    sudo apt install nodejs
    sudo apt install npm
    sudo apt install python3-pip
    git clone https://github.com/andrewcgaitskell/image-editor.git
    cd dash-template
    pip install --user pipenv
    export PATH=$PATH:/home/andrew_gaitskell/.local/bin
    echo $PATH
    sudo apt install software-properties-common
    
## installed python version

    python3 --version
    
    ### edit pipfile and add python version
    nano Pipfile
    
## install python packages

    pipenv --python 3.9.7 install pandas
    
## Jupyterlab Setting Up

    sudo npm install -g npm@8.3.0 to update
    ?? sudo npm install -g configurable-http-proxy
    sudo npm init
  
    sudo npm install configurable-http-proxy

  
# Install Jupyterlab

    pipenv --python 3.9.7 install jupyterhub


# nginx

    sudo apt update
    sudo apt install nginx
    
# add sub domain

    https://uk.godaddy.com/help/add-a-subdomain-4080
    

# add https support

## certbot

    sudo apt install certbot python3-certbot-nginx

    sudo certbot --nginx -d images.andrewcgaitskell.com


   Account registered.
Requesting a certificate for images.andrewcgaitskell.com
Performing the following challenges:
http-01 challenge for images.andrewcgaitskell.com
Waiting for verification...
Cleaning up challenges
Deploying Certificate to VirtualHost /etc/nginx/sites-enabled/default
Redirecting all traffic on port 80 to ssl in /etc/nginx/sites-enabled/default
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Congratulations! You have successfully enabled
https://images.andrewcgaitskell.com
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Subscribe to the EFF mailing list (email: andrew@gaitskell.com).
We were unable to subscribe you the EFF mailing list because your e-mail address appears to be invalid. You can try
 again later by visiting https://act.eff.org.
IMPORTANT NOTES:                                                                                                   
 - Congratulations! Your certificate and chain have been saved at:                                                 
   /etc/letsencrypt/live/images.andrewcgaitskell.com/fullchain.pem
   Your key file has been saved at:
   /etc/letsencrypt/live/images.andrewcgaitskell.com/privkey.pem
   Your certificate will expire on 2022-05-01. To obtain a new or
   tweaked version of this certificate in the future, simply run
   certbot again with the "certonly" option. To non-interactively
   renew *all* of your certificates, run "certbot renew"
 - If you like Certbot, please consider supporting our work by:
   Donating to ISRG / Let's Encrypt:   https://letsencrypt.org/donate
   Donating to EFF:                    https://eff.org/donate-le

# check sites enabled file

    sudo nano /etc/nginx/sites-enabled/default

# Create pythonuser user
 
 sudo useradd -m pythonuser
 
 sudo passwd pythonuser
 
 # Remove pythonuser user
 
 sudo userdel pythonuser

# Create Jupyterhub Config

jupyterhub --generate-config
