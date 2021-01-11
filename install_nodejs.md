# Install NodeJS

## Install through command

    curl -sL https://deb.nodesource.com/setup_10.x | sudo -E bash -  
    sudo apt-get install -y nodejs  
    sudo apt-get install -y build-essential


## Install through NPM

First install npm

    apt install npm

Update npm to lastest, then check its version

    npm install -g npm@latest
    npm -v

Install Node

    npm cache clean -f
    npm install -g n
    n stable


## Upgrade Node a specific version

While the latest is not always the most stable, we can do

    n latest
    
Or switch to a specific version

    n 12.18.3
