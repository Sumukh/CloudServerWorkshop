Cloudy with a Chance of Servers
===================
### A guide to getting started with “the cloud”. 
##### Author: Sumukh Sridhara 
---
A workshop intended for those who are new to using web server/"the cloud". 

What will this workshop cover:

1. Quick overview of the cloud (DNS, Servers, ETC)
2. How to get started with the cloud by launching a server (say on DigitalOcean). 
3. Let’s use apache to server up a webpage. 
4. Modify the pages, maybe install a personal website
5. Quickly modify the config to change an error file
6. Now let’s use something much better: Nginx. 
7. Use Nginx to serve up the page. Do a quick speed test or load test.
8. Let’s talk about AWS. What is the benefit of AWS (What do you use it for? etc)
9. Example of launching servers, using SSH authentication. S3 is for file storage. CDN 
10. What else can you do? Configure subdomains with DNS. Setup an email server. Use the server as backup. 
11. Let’s talk maintenance & keeping the server up. Scaling. NewRelic monitoring, Pingdom. How do you ensure your site stays up and fast. Use a CDN
12. By the end of the workshop you'll have a website deployed on your very own VPS.

---

### Prereqs.
1. An account at DigitalOcean (or a similiar VPS provider)
  1. You might need a credit-card for DigitalOcean but you can use promocodes to get $10 of credit - 2 months of a server. These were valid at the time of writing: SSD2014 and OMGSSD10
2. Terminal if your are on OSX or Putty if you are Windows. 
  1. Windows: You can [install Putty here](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)
  2. Windows: Connect on SSH over port 22

### Copy Pasta. 
I'll include what you need to copy & paste here and you can see my notes if you want to get ahead.

* Copy paste the IP Address and open it in your browser.
* OSX/Linux: `ssh root@IPAddressThatYouGotInTheEmail` 
  * Windows users should use Putty. 


Once you are in SSH (on your server):
```bash
sudo apt-get update
sudo apt-get install apache2 unzip git-core
```
Now go to your browser and refresh the page.
```
cd /var/www 
ls
```

```
nano index.html
```

Control-X to save once your done changing it (then confirm with y and then enter)


Refresh your browser.

```
rm index.html
```

```
wget -qO- -O tmp.zip http://html5up.net/telephasic/download && unzip tmp.zip && rm tmp.zip
```

Refresh your browser.

Now let's do a speed test [copy and paste your IP address into here](http://tools.pingdom.com/fpt/)

```
cd /etc/apache2/sites-enabled/
```

```
nano 000-default
```

Add this line: 
```
ErrorDocument 404 /index.html
``` 

It should be under `<Directory /var/www/>`

Now it should look like this. 
```
        <Directory /var/www/>
                ErrorDocument 404 /index.html
```

Then: 
```
sudo service apache2 restart
```


Now go to page that doesn't exist in your browser- so instead of index.html try /nope.html

Install PHP
```
sudo apt-get install php5 libapache2-mod-php5 php5-mcrypt
```

Optional For Now: Make index.php a valid Index file. [details] (https://www.digitalocean.com/community/articles/how-to-install-linux-apache-mysql-php-lamp-stack-on-ubuntu#stepThree)

Rip Apache Out:
```
sudo apt-get install nginx
sudo apt-get install php5-fpm
```

Try: `top` (control-c to quit)

```bash
sudo service apache2 stop && sudo service nginx start
```

```
sudo nano /etc/nginx/sites-available/default
```

```
cd /usr/share/nginx/www
```

Refresh your browser

```
rm index.html
```

```bash
wget -qO- -O tmp.zip http://html5up.net/telephasic/download && unzip tmp.zip && rm tmp.zip
```

[Repeat the speed test](http://tools.pingdom.com/fpt/)



### Things to experiment with later
* Install MySQL and use it.
* Play with PHP.
* Install Varnish to make your site even faster.
* Install python or node.js or Ruby/Ruby On Rails
* Install wordpress or a blogging platform
* Try load-testing your server.
* Setup a Domain with your site.

### Useful Links
1. [Digital Ocean's Community Articles & Tutorials](https://www.digitalocean.com/community/)
2. [How to login with Putty on Windows](https://www.digitalocean.com/community/articles/how-to-log-into-your-droplet-with-putty-for-windows-users)
3. [Pingdom Speed Test](http://tools.pingdom.com/fpt/)
4. [Amazon Web Services](http://aws.amazon.com/)
5. [Linode](http://linode.com)
6. [Rackspace](http://rackspace.com)
7. [Use SSH keys instead of passwords](https://www.digitalocean.com/community/articles/how-to-use-ssh-keys-with-digitalocean-droplets)
8. [Use fail2ban](https://www.digitalocean.com/community/articles/how-to-protect-ssh-with-fail2ban-on-ubuntu-12-04)
9. [Essential security for servers](http://plusbryan.com/my-first-5-minutes-on-a-server-or-essential-security-for-linux-servers)

#### Sources:
1. [Digital Ocean's Community Articles](https://www.digitalocean.com/community/)
