
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

# check sites enabled file

    sudo nano /etc/nginx/sites-enabled/default

