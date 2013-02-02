vagrant-localwiki
=================

`vagrant-localwiki` consists of a Vagrantfile and Chef cookbooks that launch and configure a LocalWiki server.

Usage
-----

1. [Install Vagrant.](http://vagrantup.com/v1/docs/getting-started/index.html)
2. Add a 64-bit Ubuntu 12.04 box: `vagrant box add precise64 http://files.vagrantup.com/precise64.box`
3. Create and enter a directory that will contain your LocalWiki work, e.g. `~/localwiki-project/`
4. Clone this repository: `git clone <repository>'
5. Clone the LocalWiki repository alongside this repository.
6. Create an empty localwiki_data folder, which be mounted at `/usr/share/localwiki` to store LocalWiki's data files.
7. Go into the vagrant-localwiki subdirectory: `cd vagrant-localwiki'
8. Run `git submodule update --init --recursive' to pull in submodules.
9. Run `vagrant up`.
10. Run `vagrant ssh` to access the machine. Your LocalWiki repository is mounted at `/srv/localwiki/`. The LocalWiki virtualenv is activated at login. By default, a Django superuser named `admin` is created with the password `admin`.
11. Go to `/srv/localwiki/sapling/` and run `python manage.py init_settings` to initialize your secret key and enter your CloudMade API key.

Locale issue
------------

If you get the following error:

    [2013-02-02T02:12:34+00:00] FATAL: Mixlib::ShellOut::ShellCommandFailed: bash[create_postgis_template] (geodjango::postgis line 9) had an error: Mixlib::ShellOut::ShellCommandFailed: Expected process to exit with [0], but received '1'
    ---- Begin output of "bash"  "/tmp/chef-script20130202-1151-16uzeol-0" ----
    STDOUT: 
    STDERR: createdb: database creation failed: ERROR:  encoding UTF8 does not match locale en_US
    DETAIL:  The chosen LC_CTYPE setting requires encoding LATIN1.
    ---- End output of "bash"  "/tmp/chef-script20130202-1151-16uzeol-0" ----
    Ran "bash"  "/tmp/chef-script20130202-1151-16uzeol-0" returned 1
    Chef never successfully completed! Any errors should be visible in the
    output above. Please fix your recipes so that they properly complete.

Try this:

    vagrant destroy
    vagrant up --provision-with shell
    vagrant reload

EC2 Support
-----------

The README in the `ec2/` folder explains how to launch your configuration on an EC2 server. Here's an example command to launch a server:

    ec2-run-instances ami-a29943cb --instance-type m1.small --key aws-keypair1 --user-data-file ec2/bootstrap.sh -g web -g default

License
-------

This project is a derivative work of LocalWiki's install scripts, so LocalWiki's GPL License applies. Should LocalWiki be relicensed to a compatible license in the future, you may use this code in compliance with the Apache License.

Copyright (c) 2010-2012 by Philip Neustrom <philip@localwiki.org>
Copyright (c) 2010-2012 by Mike Ivanov <mike@localwiki.org>

All rights reserved, see COPYING for details.

This program is free software; you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation; either version 2 of the License, or
(at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License
along with this program; if not, write to the Free Software
Foundation, Inc., 59 Temple Place, Suite 330, Boston, MA  02111-1307  USA

-----

Copyright 2012 by Niran Babalola

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
