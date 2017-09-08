Tequila-nginx
=============

Changes

v 0.8.XXX on YYY
----------------

* Add a [client_max_body_size option](http://nginx.org/en/docs/http/ngx_http_core_module.html#client_max_body_size).

v 0.8.2 on Sep 6, 2017
----------------------

* Provide a 'none' cert_source option (fixes #7)

* Start nginx a bit later (fixes #6)

* Add assertions about the cert_source (fixes #5)

* Use the proper X-Forwarded-Proto header
