IRR Non-Authoritative Object Cleanup Analyser
=============================================

A simple tool to show what IRR "Non Authoritative" objects are affected by RPKI ROAs. The motivation behind the tool is to help reduce the amount of RPKI Invalid IRR route objects in the IRR eco-system.

An IRR route object is validated following the Origin Validation procedure as described in [RFC 6811](https://tools.ietf.org/html/rfc6811).
The input into the procedure is the `route:` object's primary key: the prefix and the ASN value of the `origin:` attribute.

A predecessor of this tool facilitated testing the implementation of the [RIPE-731](https://www.ripe.net/publications/docs/ripe-731) policy.

Installation
------------

`pip3 install irr-nonauth-cleanup`

Use
---

`$ irr-nonauth-cleanup -i ./somedatabase.db.gz`

You can download an assortment of IRR databases from the [RADB](http://radb.net) `ftp://ftp.radb.net/radb/dbase/` public IRR mirror service.

If add `-r YOUR_IRRd_OVERRIDE_PW` as command line arguments, the program will output data in a way that can be piped straight into an email to Legacy IRRd daemons.

```
hanna:~ job$ irr-nonauth-cleanup --help
usage: irr-nonauth-cleanup [-h] [-c CACHE] -i IRR [--afi AFI] [-a ASN]
                           [-p PREFIX] [-r RPSL] [-s STATE] [-v]

optional arguments:
  -h, --help     show this help message and exit
  -c CACHE       Location of the RPKI Cache in JSON format
                 (default: https://rpki.gin.ntt.net/api/export.json)
  -i IRR         Location of the IRR database file
                 (fetch a .db.gz file from ftp://ftp.radb.net/radb/dbase/)
  --afi AFI      [ ipv4 | ipv6 | mixed ]
                 (default: mixed
  -a ASN         Limit searching to this ROA Origin ASN
  -p PREFIX      Search for specific prefix (and all its more-specifics)
  -r RPSL        Specify IRR override password and present invalids in RPSL format for deletion
  -s STATE       RPKI Origin Validation State [ valid | invalid | unknown | all ]
                 (default: invalid)
  -v, --version  show program's version number and exit
```

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
