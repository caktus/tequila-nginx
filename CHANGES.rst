Tequila-nginx
=============

Changes

v 0.8.12 on Oct 2, 2019
-----------------------

* Fix deprecation warnings with ``httpauth`` tasks


v 0.8.11 on Sep 26, 2019
------------------------

* Don't add an extra slash when redirecting to a domain in ``redirect_domains``


v 0.8.10 on Sep 6, 2019
-----------------------

* If nginx is behind a load balancer that sets X-Forwarded-Proto: http,
  redirect to HTTPS even on port 443.

v 0.8.9 on Sep 11, 2018
-----------------------

* New variables ``nginx_http_port`` and ``nginx_https_port`` to
  override the listen ports from 80 and 443.

v 0.8.8 on Jul 30, 2018
-----------------------

* New variable ``project_port`` to say that Django is listening on a port
  other than 8000, to help with multi-site deploys.

v 0.8.7 on June 15, 2018
-----------------------

* Add an additional clause to the ``force_ssl`` block in ``nginx.conf.j2``.
  An explicit check for an empty ``$http_x_forwarded_proto`` value is
  apparently necessary to ensure that non-https requests get redirected
  to http when not behind AWS load balancer. (See changes for v 0.8.3
  for details on the affected code.)

  Without this change, deploys with ``force_ssl`` to single-server environments
  may fail with a Gunicorn scheme mismatch error (in Digital Ocean).

v 0.8.6 on May 13, 2018
-----------------------

* Change the certbot cron job to fire off daily, at some random time
  of day.  Ansible will replace the parameters of the cron job each
  time it is deployed, but if you have the older cron job under a
  different name, it is recommended to remove it.  See the Let's
  Encrypt / Certbot section of README.rst for instructions.


v 0.8.5 on Sep 22, 2017
-----------------------

* Add a new optional variable, ``additional_domains``, which are then
  appended to a list containing ``domain`` and then injected into the
  nginx template to support access of the site under multiple domain
  names.

* Add a new optional variable, ``redirect_domains``, which then
  trigger a permanent redirect back to the host at ``domain``,
  e.g. for redirecting www to non-www.


v 0.8.4 on Sep 13, 2017
-----------------------

* Add a `client_max_body_size option <http://nginx.org/en/docs/http/ngx_http_core_module.html#client_max_body_size>` option.


v 0.8.3 on Sep 12, 2017
-----------------------

* Use the full path to certbot-auto, so cron can properly run it.

* Only redirect port 80 requests if the forwarded protocol wasn't
  https.  This allows for the case where SSL is terminated at an
  external load balancer, as in AWS ELB.

* Allow forcing SSL if the cert_source is 'none'.  This also allows
  for the external load balancer case.


v 0.8.2 on Sep 6, 2017
----------------------

* Provide a 'none' cert_source option (fixes #7)

* Start nginx a bit later (fixes #6)

* Add assertions about the cert_source (fixes #5)

* Use the proper X-Forwarded-Proto header
