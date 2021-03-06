class: center, middle

background-image: url(images/crowd.jpg)

![Ents24 Logo](images/logo.png)

# Vagrant & Puppet
## Tips & Tricks

---
class: table-list, center

--

* ![](images/icons/ubuntu.png)
* ![](images/icons/ubuntu.png)
* ![](images/icons/ubuntu.png)
--

* ![](images/icons/windows.png)
* ![](images/icons/windows.png)
--

* ![](images/icons/mac.png)
--

* ![](images/icons/php.png)
* ![](images/icons/node.png)
--

* ![](images/icons/mysql.png)
* ![](images/icons/elasticsearch.png)
--

* ![](images/icons/phing.png)
* ![](images/icons/sencha.png)
--

* ![](images/icons/memcached.png)
--

* ![](images/icons/apache.png)
--

* ![](images/icons/stackoverflow.png)

--

#Why we use Vagrant & Puppet

---
class: center
#Overview
.left[
* Vagrant - CLI for virtual machines
* Puppet - Configuration & software management
]
.left[
* Vagrantfile
* Manifests & Modules
* Version control your development environment
]
---
class: center, middle
background-image: url(images/puphpet.png)

# Getting Started
Using PuPHPet
---

![](images/puphpet-screenshot.png)

---
class: center, middle
#Customising

Let's install selenium RC in our VM
---

![](images/puppetforge.png)

---

Puppetfile :
```coffeescript
mod 'jhoblitt/selenium'
	mod 'rodjek/logrotate' #Dependency for selenium
```

default.pp:
```ruby
class { 'selenium::server':
  display      => ':99',
}
```

```c#
C:\Users\Doug\Code\vagrant>vagrant provision
```
---
class: center, middle
#YAML
1 minute SSL VHost

---

```coffeescript
apache:
    vhosts:
        "%{::vm_hostname}": &ents24
            servername: "%{::vm_hostname}"
            serveraliases:
                - "%{::host_hostname}.local.ents24.com"
            docroot: /var/www/
            port: '80'
            directories:
                - path: /var/www/
                  allow_override: all
                - path: /var/www/ents24/Web/
                  fallbackresource: /ents24/Web/index.php
            request_headers:
                - set Served-As "HTTP"
```
--

```coffeescript
        #This SSL vhost is a reference to the one above,
		#and overrides some settings
        "%{::vm_hostname}-ssl":
            <<: *ents24
            ssl: true
            port: 443
            ssl_cert: '/etc/ssl/ents24/ents24-dev.crt'
            ssl_key: '/etc/ssl/ents24/ents24-dev.key'
            request_headers:
                - set Served-As "HTTPS"
```
---

```coffeescript
apache:
    vhosts:
*        "%{::vm_hostname}": &ents24
            servername: "%{::vm_hostname}"
            serveraliases:
                - "%{::host_hostname}.local.ents24.com"
            docroot: /var/www/
            port: '80'
            directories:
                - path: /var/www/
                  allow_override: all
                - path: /var/www/ents24/Web/
                  fallbackresource: /ents24/Web/index.php
            request_headers:
                - set Served-As "HTTP"
```
```coffeescript
        #This SSL vhost is a reference to the one above,
		#and overrides some settings
        "%{::vm_hostname}-ssl":
*            <<: *ents24
            ssl: true
            port: 443
            ssl_cert: '/etc/ssl/ents24/ents24-dev.crt'
            ssl_key: '/etc/ssl/ents24/ents24-dev.key'
            request_headers:
                - set Served-As "HTTPS"
```
---
#Shared Folder Speed

* NFS (root)
* Samba (root)
* VMWare (money)
* 
---
class: center, middle
#Port Forwarding

---
#Windows

```ruby
  host_port     = Vagrant::Util::Platform.windows? ? 80  : 8080
  host_port_ssl = Vagrant::Util::Platform.windows? ? 443 : 8443

  config.vm.network "forwarded_port", guest: 80,  host: host_port
  config.vm.network "forwarded_port", guest: 443, host: host_port_ssl
```

.center[
![](images/windows-port.png)
]

---
#Linux (rinetd)

```
sudo apt-get install rinetd
```

/etc/rinetd.conf:
```
# bindadress bindport connectaddress connectport
192.168.2.1 80 192.168.2.3 80
192.168.2.1 443 192.168.2.3 443
```

---
#OSX (pf)

Anchor File:
```
rdr pass on lo0 inet proto tcp 
	from any to 127.0.0.2 port 80 -> 127.0.0.1 port 8080
```

PF Config:
```
rdr-anchor "forwarding"
load anchor "forwarding" from "/etc/pf.anchors/<anchor file>"
```

Sysctl :
```
net.inet.ip.forwarding=1
net.inet6.ip6.forwarding=1
```

Launch list :
```
<key>ProgramArguments</key>
<array>
	<string>pfctl -e -f /etc/pf.conf</string>
</array>
```

---
class: center, middle
#Golden Master

---
class: center
#Puppet is Idempotent

p = Puppet Manifest

x = System State

![](images/idempotent.png)
