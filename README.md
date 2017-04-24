# a2addsite
Yet another apache2 virtualhost creator, and then some.

## Requirements
- sudo access
- apache2 web server
- [a2ensite](http://man.he.net/man8/a2ensite) command along with sites-available / sites-enabled directory layout

If you're on a Debian based linux distro and have apache2 installed, you're probably all set. If you're not, it is not that hard to make your distro meet these requirements, just google around.

The script intends to be flexible enough, via configuration parameters, to accomodate to non-Debian scenarios.

## What's in it for me?

Give birth to a new virtualhost with just the run of a command.

And then some? the idea of each virtualhost being a *project* is at the heart of this script's logic. No more going to one place for your vhost apache logs, another place for your vhost config and another for your source code. By creating your vhost with this script you get a directory structure created to contain anything related to this new project of yours:

- A configuration directory to store your apache virtualhost configuration file (init with some defaults, you take it from here)
- A logs directory to store a symlink to where your vhost's apache logs live
- A source directory, which will be the root of your vhost, with an index file to test it out right away

## Installation
1. Clone this repository
2. `sudo cp a2addsite/a2addsite /usr/local/bin/`
3. `sudo ln -s /usr/local/bin/a2addsite /bin/a2addsite`
4. `sudo chmod +x  /usr/local/bin/a2addsite`

## Configuration
1. `cp a2addsite/.a2addsite.sample ~/.a2addsite`
2. Edit ~/.a2addsite making sure the configuration values match your system and preferences (use comments in the file as guidance)

## Usage
`sudo a2addsite --proj_dir [PROJ_DIR] --proj_name [PROJ_NAME] --domain_name [DOMAIN_NAME]`

**PROJ_DIR:** the absolute path to the directory under which you want the project's directory to be created. **Optional**, can be provided via configuration file

**PROJ_NAME:** the name for the directory that will hold the project's data

**DOMAIN_NAME:** will be used for setting the ServerName in the virtualhost configuration

**I.e:**

`sudo a2addsite --proj_dir /home/user/my-projects --proj_name coolProject --domain_name coolproj.com`

Then, assuming *coolproj.com* resolves to your web server's ip address and you have enabled the vhost and reloaded apache when prompted by the script, your server should respond with the sample index page to incoming GET requests for *coolproj.com*