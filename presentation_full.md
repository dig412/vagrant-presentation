
class: center, middle

# Vagrant + PHP: 
## Beyond PuPHPet
![PuPHPet Logo](images/combo-logo.png)

---
class: center, middle

background-image: url(images/crowd.jpg)

![Ents24 Logo](images/logo.png)

# Ticket Shop & Gig Guide

PHP & MySQL, since 1999.

---
#What is Vagrant?

* CLI interface to VirtualBox (Or VMWare, or HyperV...)

---
#Why we use Vagrant

* 6 Developers
  * 3 Linux
  * 2 Windows
  * 1 Mac

* 11 Software Packages
  * Apache
  * PHP
  * MySQL
  * MemcacheD
  * BeanstalkD
  * SupervisorD
  * ImageMagick
  * Phing
  * PHPUnit
  * UglifyJs
  * Clean-CSS

.right.middle[= 36 packages required across the team]

---
# Getting Started

* PuPHPet

---
#Customising

* Extra Modules
* Heira Config

---
#Pain Points - Port Forwarding

* Windows (Yay)
* rinetd (OK)
* ipfw (Boo)

---
#Pain Points - Module Changes

This has changed recently in PuPHPet, so you may not find it.
Talk about librarian / r10k.

---
#Pain Points - Confusion

People can't remember if they're logged into the VM or not/

---
#Pain Points - Provision Speed

See golden master later

---
#Pain Points - Folder Speed

* NFS (root)
* Samba (root)
* VMWare (money)

---
#Pro Tips - Golden Master

---
#Pro Tips - SSL

---
#Pro Tips - GUI

---
#Pro Tips - Custom Module

This talk will be about using vagrant

```
<?php
namespace Ents24\Stuff
use Doug\Package;

$p = new Doug();

$p->run();
```


---

```cs
PS C:\Users\Doug\Code\vagrant-presentation\images> git status
# On branch master
#
# Initial commit
#
# Changes to be committed:
#   (use "git rm --cached <file>..." to unstage)
#
#       new file:   combo-logo.png
#       new file:   crowd.jpg
#       new file:   logo.png
#
# Untracked files:
#   (use "git add <file>..." to include in what will be committed)
#
#       logo-8b7a4912.png
#       puphpet.png
#       virtualbox-logo.png
PS C:\Users\Doug\Code\vagrant-presentation\images> git commit -m "Initial version with webfonts and logos"
```
---


#Words

Ents24 lgoo
