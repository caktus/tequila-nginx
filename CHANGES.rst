Tequila-nginx
=============

Changes

v 0.8.3 on Sep 12, 2017
-----------------------

* Use the full path to certbot-auto, so cron can properly run it.

* Only redirect port 80 requests if the forwarded protocol wasn't
  https.  This allows for the case where SSL is terminated at an
  external load balancer, as in AWS ELB.


v 0.8.2 on Sep 6, 2017
----------------------

* Provide a 'none' cert_source option (fixes #7)

* Start nginx a bit later (fixes #6)

* Add assertions about the cert_source (fixes #5)

* Use the proper X-Forwarded-Proto header
