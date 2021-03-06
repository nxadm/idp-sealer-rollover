# Shibboleth IdP3 Data Sealer Rollover.

[![Build Status](https://travis-ci.org/KULeuven-CCIS/idp-sealer-rollover.svg?branch=master)](https://travis-ci.org/KULeuven-CCIS/idp-sealer-rollover)

idp-sealer-rollover is a helper program for the Open Source
[Shibboleth IdP 3](https://shibboleth.net/products/identity-provider.html)
SAML Identity Provider.

The program does a rollover of the data sealer files and uploads them to the
target servers. Its main use case is in a clustering mode when several
Shibboleth IdP 3 backends share the same data sealer. Ideally it should be
run from an scheduler like cron (cron file included as
[idp-sealer-rollover.cron](idp-sealer-rollover.cron)).

The Shibboleth IdP 3 binaries needed to create and rollover the data sealer
files are encapsulated with Docker. The size of the
[image](https://hub.docker.com/r/kuleuvenccis/idp-sealer-rollover) is small by
using Alpine Linux and only keeping the IdP files needed for the key
management. Therefore, the deployment machines (not the target machines),
must have Docker installed. In case you don't want to use the image on the
Docker Hub, you can create your own with the
[Dockerfile in the /utils directory](utils/Dockerfile).

The [idp-sealer-rollover](idp-sealer-rollover) is an executable created from
the source in [src/](src/idp-sealer-rollover.pl) and it includes all the
dependencies ([YAML::Tiny](https://metacpan.org/pod/YAML::Tiny)). There is no
need to install the dependencies separately.

This project is hosted and used by the [KU Leuven University](https://www.kuleuven.be).

# Usage

```
idp-sealer-rollover:
Roll over Idp sealer keys using an IdP docker image, version x.x.x.
Bugs to https://github.com/nxadm/idp-sealer-rollover.

Usage:
    idp-sealer-rollover <project> <environment> [-c <configuration file>]

Parameters:
    -c|--config: configuration file
    (default: environment variable $IDP_SEALER_ROLLOVER_CONFIG)
    -h|--help:   this help info

```

E.g.
```
$ idp-sealer-rollover idp test
$ idp-sealer-rollover idp quality
$ idp-sealer-rollover idp production
```

# Configuration

A commented configuration is included as
[idp-sealer-rollover.yaml](idp-sealer-rollover.yaml).


