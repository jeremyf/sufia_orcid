# Sufia Orcid

*NOTE: This is not suitable for a Production environment.*

Welcome to a reference implementation for leveraging the Sufia and Orcid gems.

The [Sufia gem](https://github.com/projecthydra/sufia) is a [Project Hydra](https://projecthydra.org) [Rails Engine](http://edgeguides.rubyonrails.org/engines.html) for self-deposit institutional repositories.

The [Orcid gem](https://github.com/projecthydra-labs/orcid) is a Rails Engine for integrating with [Orcid.org](https://orcid.org)

## Current State of Things

This is being prepared for a May 21st, 2014 meeting in Chicago.
**I do not have plans to keep this reference up to date.**

## Getting started

Running this application locally: (*Note: this assumes you have Rails ready environment*)

1. Review the [Orcid gem's README](https://github.com/projecthydra-labs/orcid/blob/master/README.md).
It provides instructions for registering your application.
1. Generate a [self-signed SSL certificate](http://www.akadia.com/services/ssh_test_certificate.html).
1. Run `$ bundle install`
1. Run `$ rake bootstrap`
1. Update `./config/application.yml` with your ORCID application credentials.

At this point you should be ready.

1. Run `$ thin start -p 3000 --ssl --ssl-key-file server.key --ssl-cert-file server.crt`
1. In your browser of choice, go to [https://localhost:3000](https://localhost:3000)
1. Click on "[Login](https://localhost:3000/users/sign_in)"
  1. Your credentials - which can be found in `./db/seeds.rb` - are:
    1. *Email:* orcid@sufia.org
    1. *Password:* icanhazorcid
1. Edit your profile
  1. Click on your email in the top right corner
  1. Then click "[Edit your Profile](https://localhost:3000/users/orcid@sufia-dot-org/edit)"

You can now interact with the Orcid widget by:

* Looking up your existing ORCID
* Creating an ORCID


*
* Generate a self-signed SSL certificate with a key file of `server.key` and cert file of `server.crt`.
* Start the server with thin `thin start -p 3000 --ssl --ssl-verify --ssl-key-file server.key --ssl-cert-file server.crt`
