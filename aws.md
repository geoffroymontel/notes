# AWS memo

## Key pair
Save your `awskeypair.pem` file !!

## AWS EC2 Console
https://console.aws.amazon.com/ec2/

Launch an Ubuntu instance and then connect it via ssh

```bash
ssh -l ubuntu-i awskeypair.pem root@ec2-54-228-3-103.eu-west-1.compute.amazonaws.com 
```

A terminated instance will disappear after a while, just give it some time

