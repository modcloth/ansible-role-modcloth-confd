modcloth.confd
========

This role installs and configures confd (and allows adding of confd resources/templates).

It:
- Installs confd
- Optionally creates confd resources and templates
- Installs a cron task to run confd

See https://github.com/kelseyhightower/confd for description of confd.

Requirements
------------

None

Role Variables
--------------

See `defaults/main.yml` for defaults.

```yml
confd_version: # version of confd to download
confd: # confd remote filename
confd_download: # url to download confd from
confd_home: # where to put the confd binary
confd_config: # where to store confd configuration
confd_backend: # which confd backend to use
confd_backend_nodes: # list of confd backend nodes

# list of confd resources
# these are used to generate confd resource.toml's and templates to use during configuration generation
confd_resources: []
# each resource is a hash with the following keys:
# service_name (required): name of the service which uses the confd generated configuration
# template (required): name of the local template to copy up (using copy module)
# check_cmd (optional): the command to run to check if the generated file is valid (defaults to true)
# reload_cmd (optional): the command to run to have the service reload the configuration (defaults to "sudo service {{service_name}} restart"
# owner (optional): user who should own the generated file (defaults to root)
# group (optional): group who should own the generated file (defaults to root)
# mode (optional): the file mode of the generated file (defaults to 0644)
# template_name (optional): name of the template on the remote system (defaults to {{service_name}}.conf.tmpl)
# template_output (optional): "{{nrmysql_location.stdout}}/config/plugin.json"
# confd_keys (optional): list of keys for confd to check
```

Dependencies
------------

None

Example Playbook
-------------------------

```yml
- hosts: all
  roles:
  - role: modcloth.confd
    confd_resources:
    - service_name: foo
      template: "files/foo.tmpl"
      template_output: /etc/defaults/foo
      confd_keys:
      - /myapp
```

License
-------

MIT

Author Information
------------------

ModCloth, Inc.