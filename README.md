# Ansible Role: Passenger

Installs Passenger (with Nginx) on RedHat/CentOS or Debian/Ubuntu linux servers.

## Requirements

None.

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

#### Nginx Virtual Host
Nginx virtual hosts are written to `/etc/nginx/sites-available`, and symlinked to `/etc/nginx/sites-enabled`.
The `/etc/nginx/nginx.conf` file includes a directive to read all files in the sites-enabled directory.  
This modules contains a generic vhost template that includes the following variables.

The server name (used in the Nginx virtual host configuration).

    passenger_server_name: www.example.com

The `passenger_root` for your application (e.g. the `public` folder in a rails app).

    passenger_app_root: /opt/example/public

The app environment passenger will load.

    passenger_app_env: production

This module also allows a user to pass in a custom template.
To enable this feature, set the `nginx_vhost_template` variable,
and place the template in the `"{{ playbook_dir }}/templates"` directory.

    nginx_vhost_template: some_custom_template

Be sure that the template has a `.j2` extension, but do not include it in the `nginx_vhost_template` variable.  
Custom templates are not constrained to the variables listed above for the generic template.  

#### Nginx Configuration Variables
Values for passenger configuration directives inside `passenger.conf` on RHEL or `nginx.conf` on Debian.
These defaults should generally work correctly, but if you build `ruby` on its own (as an example), the path to ruby may be different.

    passenger_root: /usr/lib/ruby/vendor_ruby/phusion_passenger/locations.ini
    passenger_ruby: /usr/bin/ruby

Nginx directives, these are all in the `nginx.conf` file.

    nginx_user: 'nginx'
    nginx_group: 'nginx'
    nginx_worker_processes: "4"
    nginx_worker_connections: "768"
    nginx_keepalive_timeout: "65"
    
Some installations of nginx include a default virtual host.  
By default, this module removes it. To change this behavior, set `nginx_remove_default_vhost` to `false`.

    nginx_remove_default_vhost: false

## Dependencies

None.

## Example Playbook

    - hosts: server
      roles:
        - { role: erumble.passenger }

## License

MIT / BSD

## Author Information

This role was created in 2015 by [Jeff Geerling](http://jeffgeerling.com/), author of [Ansible for DevOps](http://ansiblefordevops.com/).  
And was later edited by Eric Rumble in 2016.
