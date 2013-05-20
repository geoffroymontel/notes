# Memo Puppet

## Introduction

Puppet is written in the Ruby language, which means that you must have Ruby installed on your VM.
The best is to install RVM right from the start.

0. Update Linux
```
sudo apt-get update
sudo apt-get upgrade
```

1. Install Git and build-essentials
```
sudo apt-get install build-essential git-core curl
```

2. Install RVM
```
curl -L get.rvm.io | bash -s stable
```

Read the output to know how to start using rvm.

Then install what 
```
rvm requirements
```
and 
```
rvm notes
```
say

3. Install Ruby
```
rvm install ruby-1.9.3-p392
rvm use 1.9.3 --default
ruby -v
``

## Installing puppet

```
wget http://apt.puppetlabs.com/puppetlabs-release-precise.deb
sudo dpkg -i puppetlabs-release-precise.deb
sudo apt-get install puppet
```



