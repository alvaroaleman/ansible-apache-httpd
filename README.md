# ansible-apache-httpd

## Description

This role manages the Apache HTTP Server

## Requirements

* EL7

## Role Variables

* ``httpd_modules``: List of modules to install and enable, without the mod prefix(list, default: ``[]``)
* ``httpd_default_template``: The template to use if a vhost doen't have one specified (string)
* ``httpd_default_vhost_mode``: The octal permissions to use as default for vhosts (string, default: ``0644``)
* ``httpd_listen_ip``: The IP to listen on (string, default: ``'127.0.0.1'``)
* ``httpd_listen_port``: The port to listen on (int, default: ``80``)

### httpd_vhosts

``httpd_vhosts`` is a list of vhosts to deploy.

    httpd_vhosts:
      - name: myvhost
        template: mytemplate.j2     #Defaults to httpd_default_template if omitted
        mode: 0600                  #Defaults to httpd_default_vhost_mode if omitted
        myownvar: HelloWorld!       #You can define your own elements and access them from the template using {{ item.varname }}

### httpd_sebooleans

``httpd_sebooleans`` is a list of sebooleans to adjust.

    httpd_sebooleans:
      - name: httpd_can_connect_ldap
        state: false              #Defaults to true if unset

## Example Playbook

    - hosts: all
      roles:
         - { role: ansible-apache-httpd }

## Contributing

If you want to contribute to this repository please be aware that this
project uses a [gitflow](http://nvie.com/posts/a-successful-git-branching-model/)
workflow with the next release branch called ``next``.

Please fork this repository and create a local branch split off of the ``next``
branch and create pull requests back to the origin ``next`` branch.

## License

Apache Version 2.0

## Integration testing

This role provides integration tests using the Ruby RSpec/serverspec framework
with a few drawbacks at the time of writing this documentation.

Running integration tests requires a number of dependencies being
installed. As this role uses Ruby RSpec there is the need to have
Ruby with rake and bundler available.

    # install role specific dependencies with bundler
    bundle install

<!-- -->

    # run the complete test suite with Docker
    rake suite

<!-- -->

    # run the complete test suite with Vagrant
    source  envvars-vagrant.sample
    rake suite

    # run the complete test suite with Vagrant without destroying the box afterwards
    source  envvars-vagrant.sample
    RAKE_ANSIBLE_VAGRANT_DONT_CLEANUP=1 rake suite


## Author information

Alvaro Aleman


<!-- vim: set nofen ts=4 sw=4 et: -->
