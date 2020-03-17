IRR-NONAUTH Cleanup Analyser
=====================================

A simple tool to show what IRR "Non Authoritative" objects are affected by RPKI ROAs.

An IRR route object is validated following the Origin Validation procedure as described in [RFC 6811](https://tools.ietf.org/html/rfc6811).
The input into the procedure is the `route:` object's primary key: the prefix and the ASN value of the `origin:` attribute.

A predecessor of this tool facilitated testing the implementation of the [RIPE-731](https://www.ripe.net/publications/docs/ripe-731) policy.

Installation
------------

`pip3 install irr-nonauth-cleanup`

Use
---

`$ irr-nonauth-cleanup -i ./somedatabase.db.gz`

You can download an assortment of IRR databases from [RADB](ftp://ftp.radb.net/radb/dbase/)'s public IRR mirror service.

Copyright
---------

Copyright (c) 2020 Job Snijders <job@ntt.net>
