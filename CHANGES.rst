Tequila-nginx
=============

Changes

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
