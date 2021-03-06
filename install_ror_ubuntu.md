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

Make rvm ruby the default :
```
rvm use 1.9.3 --default
```

## Install additional packages

Follow what's written in :
```
rvm requirements
```

## Install Ruby & Rails
Remove ri & rdoc installation by default
```
subl .gemrc
```
and add the following lines :
```
install: --no-rdoc --no-ri
update: --no-rdoc --no-ri
```

Then follow the instructions here :
https://rvm.io/rvm/install/

`~.bash_login` is not loaded by default on Ubuntu, so you need to edit `.bashrc` and add at the bottom :
```
source ~/.bash_login
```
Restart your shell and check rails is here :
```
rails -v
```

## Install nodejs
You will need it for Rails!
```
sudo apt-get install nodejs
```

## Install postgres

Ǹot sure about that...

* Install postgresql and libpq-dev
```
sudo apt-get install postgresql libpq-dev
```
* Install the GUI
```
sudo apt-get install pgadmin3
```
* Change postgres user password and restart
```
sudo -u postgres psql  
\password postgres  
<enter password twice>  
\q  
sudo /etc/init.d/postgresql reload  
```

* change psql authentication
```
sudo vi /etc/postgresql/9.1/main/pg_hba.conf
```

Find the line :
```
local   all             all                                     peer
```

And replace it with :
```
local   all             all                                     md5
```

Then restart the server
```
sudo service postgresql restart
```

## Test the install
* Create a database
Name of application: test_app  
Name of database user: test_app  
Password of database user: apple  
Name of database: test_app_development  

```
sudo -u postgres createuser -P  
> Enter name of role to add: test_app  
> Enter password for new role: apple  
> Enter it again: apple  
> Shall the new role be a superuser? (y/n) n  
> Shall the new role be allowed to create databases? (y/n) n  
> Shall the new role be allowed to create more new roles? (y/n) n  
> Password: your-postgres-user-password  

sudo -u postgres createdb -O test_app test_app_development  
```

* Set up new Rails app

```
rails new test_app -d postgresql  
cd test_app  
bundle install  
```

* You have to store the password in your system :
```
subl ~/.pgpass
```

Add the password :
```
localhost:*:*:test_app:apple
```

Then chmod and try to connect to your database, no password should be needed :
```
chmod 0600 ~/.pgpass
psql test_app_development -U test_app
```

* Try a scaffold : 
```
rails generate scaffold User name:string   email:string  
rake db:migrate  
rails s  
```

And point your browser to :

http://localhost:3000/users

It should work!

# Extra bits

## Install ffmpeg
```
sudo apt-get install ffmpeg
```

## Install imagemagick
```
sudo apt-get install imagemagick libmagickcore-dev libmagickwand-dev
```
