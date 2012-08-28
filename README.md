vagrant-localwiki
====================

`vagrant-localwiki` consists of a Vagrantfile and Chef cookbooks that launch and configure a LocalWiki server.

Usage
-----

1. [Install Vagrant.](http://vagrantup.com/v1/docs/getting-started/index.html)
2. Add a 64-bit Ubuntu 12.04 box: `vagrant box add precise64 http://files.vagrantup.com/precise64.box`
3. Create and enter a directory that will contain your LocalWiki work, e.g. `~/localwiki-project/`
4. Clone this repository.
5. Clone the LocalWiki repository alongside this repository.
6. Create an empty localwiki_data folder, which be mounted at `/usr/share/localwiki` to store LocalWiki's data files.
7. Run `vagrant up`.
8. Run `vagrant ssh` to access the machine. Your LocalWiki repository is mounted at `/srv/localwiki/. The LocalWiki virtualenv is activated at login. By default, a Django superuser named `admin` is created with the password `admin`.
9. Go to `/srv/localwiki/sapling/` and run `python manage.py init_settings` to initialize your secret key and enter your CloudMade API key.