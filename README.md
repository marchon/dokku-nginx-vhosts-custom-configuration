# dokku-nginx-vhosts-custom-configuration

[Dokku](https://github.com/progrium/dokku) plugin to add custom configuration directives to the nginx vhost configuration on the dokku host.

This plugin adds a new dokku command

## Usage

nvcc        # nginx vhost custom configuration 

`nvcc:nginx.conf` will display the current nginx.conf


`nvcc:nginx.conf.d` will display the current nginx.conf.d/ directory contents


`nvcc:nginx-vhosts-custom-configuration.conf` will display the current nginx.conf.d/nginx-vhosts-custom-configuration.conf contents


`nvcc:port` will display the current container port




## Background

Relevant use cases for when the nginx vhost configuration needs to be customized can be to set proxy timeouts in order to allow long running requests, setting specific SSL directives, enabled uploading of large files and the like.


nginx.inc.conf

## Installation

WARNING: if using dokku-alt rather than dokku 

make sure that you have a symlink in /var/lib/dokku/plugins/ to /var/lib/dokku-alt/plugins/ 

```bash
mkdir /var/lib/dokku/
ln -s /var/lib/dokku-alt/plugins/ /var/lib/dokku/plugins/
```

Clone Plugin from Github

```bash
git clone https://github.com/marchon/dokku-nginx-vhosts-custom-configuration.git /var/lib/dokku/plugins/nginx-vhosts-custom-configuration
```

## Simple usage

1. Add a file containing your custom configuration to your app repo. For instance, you can call it `nginx.inc.conf` and commit it in the root of your app's repository.

2. Set the environment variable NGINX_VHOSTS_CUSTOM_CONFIGURATION to the in-container path to the file above:

```bash
$ dokku config:set <app> NGINX_VHOSTS_CUSTOM_CONFIGURATION=nginx.inc.conf             # Server side
$ ssh dokku@server config:set <app> NGINX_VHOSTS_CUSTOM_CONFIGURATION=nginx.inc.conf  # Client side
```

You're done! This plugin will read app environment variable with in-container path to custom configuration file and import the custom configuration to the app-specific configuration on the  dokku host.

## Additional commands

`nvcc:nginx.conf` will display the current nginx.conf

```bash
$ dokku nvcc:nginx.conf <app>             # Server side
$ ssh dokku@server nvcc:nginx.conf <app>  # Client side
```

`nvcc:nginx.conf.d` will display the current nginx.conf.d/ directory contents

```bash
$ dokku nvcc:nginx.conf.d <app>             # Server side
$ ssh dokku@server nvcc:nginx.conf.d <app>  # Client side
```

`nvcc:nginx-vhosts-custom-configuration.conf` will display the current nginx.conf.d/nginx-vhosts-custom-configuration.conf contents

```bash
$ dokku nvcc:nginx.conf.d <app>             # Server side
$ ssh dokku@server nvcc:nginx.conf.d <app>  # Client side
```

`nvcc:port` will display the current container port

```bash
$ dokku nvcc:port <app>             # Server side
$ ssh dokku@server nvcc:port <app>  # Client side
```

## License
MIT
