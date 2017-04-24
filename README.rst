tequila-nginx
=============

This repository holds an `Ansible <http://www.ansible.com/home>`_ role
that is installable using ``ansible-galaxy``.  This role contains
tasks used to install and set up an nginx webserver for a Django
deployment.  It exists primarily to support the `Caktus Django project
template <https://github.com/caktus/django-project-template>`_.


License
-------

This Ansible role is released under the BSD License.  See the `LICENSE
<https://github.com/caktus/tequila-nginx/blob/master/LICENSE>`_ file
for more details.


Contributing
------------

If you think you've found a bug or are interested in contributing to
this project check out `tequila-nginx on Github
<https://github.com/caktus/tequila-nginx>`_.

Development sponsored by `Caktus Consulting Group, LLC
<http://www.caktusgroup.com/services>`_.


Installation
------------

Create an ``ansible.cfg`` file in your project directory to tell
Ansible where to install your roles (optionally, set the
``ANSIBLE_ROLES_PATH`` environment variable to do the same thing, or
allow the roles to be installed into ``/etc/ansible/roles``) ::

    [defaults]
    roles_path = deployment/roles/

Create a ``requirements.yml`` file in your project's deployment
directory ::

    ---
    # file: deployment/requirements.yml
    - src: https://github.com/caktus/tequila-nginx
      version: 0.1.0

Run ``ansible-galaxy`` with your requirements file ::

    $ ansible-galaxy install -r deployment/requirements.yml

or, alternatively, run it directly against the url ::

    $ ansible-galaxy install git+https://github.com/caktus/tequila-nginx

The project then should have access to the ``tequila-nginx`` role in
its playbooks.


Variables
---------

The following variables are made use of by the ``tequila-nginx``
role:

- ``project_name`` **required**
- ``domain`` **required**
- ``root_dir`` **default:** ``"/var/www/{{ project_name }}"``
- ``public_dir`` **default:** ``"{{ root_dir }}/public"``
- ``static_dir`` **default:** ``"{{ root_dir }}/public/static"``
- ``media_dir`` **default:** ``"{{ root_dir }}/public/media"``
- ``nginx_conf_template`` **default:** ``"nginx.conf.j2"``
- ``ssl_dir`` **default:** ``"{{ root_dir }}/ssl"``
- ``force_ssl`` **default:** ``true``
- ``http_auth`` **default:** empty list
- ``auth_file`` **default:** ``"{{ root_dir }}/.htpasswd"``
- ``dhparams_file`` **default:** ``"{{ ssl_dir }}/dhparams.pem"``
- ``dhparams_numbits`` **default:** ``2048``
- ``cert_source`` **required, values:** ``'letsencrypt'``, ``'selfsign'``, ``'provided'``
- ``admin_email`` **required if cert_source = letsencrypt**
- ``ssl_cert`` **required if cert_source = provided**
- ``ssl_key`` **required if cert_source = provided**
- ``letsencrypt_domains`` **default:** ``[domain, 'www.'+domain]``
- ``use_memcached`` **default:** ``true``
- ``app_minions`` **required:** combined list of web servers and celery worker servers

The ``app_minions`` variable can be constructed from Ansible's
inventory information, like ::

    app_minions: "{{ groups['web'] | union(groups['worker']) }}"

in one of your project's variable files.

The ``http_auth`` variable is meant to be a list of dicts, where each
dict contains a login and password.  So, a typical definition in an
actual project might look like ::

    http_auth:
      - login: user1
        password: password1
      - login: user2
        password: password2

The ``nginx_conf_template`` variable is to allow the template that
ships with this role to be overridden, if more complex directives need
to be supported.
