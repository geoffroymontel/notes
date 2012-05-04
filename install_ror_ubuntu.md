# Installing RoR on Ubuntu 12.04TLS

## Install Sublime Text 2
Get the latest version here :
http://www.sublimetext.com/dev

Then :
```
cd ~ 
mkdir bin
cp Downloads\Subl... bin/
cd bin
tar xjf Subl...
rm Subl...bz2
ln -s Subl.../sublime_text subl
```

`~/bin` should be in your PATH. 

## Install GIT
```
sudo apt-get install build-essential git-core curl
git --version
``` 
Then set up your keys
http://help.github.com/linux-set-up-git/

## Install RVM
https://rvm.io/rvm/install/

It should be as easy as :
```
curl -L get.rvm.io | bash -s stable
```
Then restarting your console.

## Install additional packages

Follow what's written in :
```
rvm requirements
```

## Install Ruby & Rails
Follow the instructions here :
https://rvm.io/rvm/install/

`~.bash_login` is not loaded by default on Ubuntu, so you need to edit `.bashrc` and add at the bottom :
```
source ~/.bash_login
```
Restart your shell and check rails is here :
```
rails -v
```


