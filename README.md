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

Example output
--------------

```
VALID: IRR route object "203.69.138.0/24AS20940" matches ROA 203.69.138.0/24, MaxLength 24, Origin AS20940 (apnic)
NOT-FOUND: IRR route object "168.143.241.0/24AS20940" is not covered by any ROAs
INVALID! IRR route object 204.245.152.64/26AS20940 has conflicts:

    route:      204.245.152.64/26
    descr:      Akamai
    origin:     AS20940
    mnt-by:     AKAM1-ALTDB-MNT
    changed:    ablock@akamai.com 20120402
    source:     ALTDB

    Above non-authoritative IRR object is in conflict with this ROA:
        ROA: 204.245.128.0/18, MaxLength: 18, Origin AS2914 (arin)

VALID: IRR route object "203.69.141.0/24AS20940" matches ROA 203.69.141.0/24, MaxLength 24, Origin AS20940 (apnic)
VALID: IRR route object "210.61.248.0/23AS20940" matches ROA 210.61.248.0/23, MaxLength 23, Origin AS20940 (apnic)
NOT-FOUND: IRR route object "203.69.141.0/24AS20940" is not covered by any ROAs
```

Copyright
---------

Copyright (c) 2020 Job Snijders <job@ntt.net>
