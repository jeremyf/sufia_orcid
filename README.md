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
It provides [instructions for registering your application](https://github.com/projecthydra-labs/orcid/blob/master/README.md#registering-for-an-orcid-application-profile).
1. Generate a [self-signed SSL certificate](http://www.akadia.com/services/ssh_test_certificate.html) (steps 1–4).
  1. The instructions assume your certificate filenames will be `server.key` and `server.crt`
1. Run `$ bundle install`
1. Create your own application configuration `$ cp ./config/application.yml.example ./config/application.yml` and update it with your ORCID application credentials.
1. Run `$ rake bootstrap`

At this point you should be ready.

1. Start Jetty `$ rake jetty:start`
1. Start the application `$ bundle exec thin start -p 3000 --ssl --ssl-key-file server.key --ssl-cert-file server.crt`
  1. *If you use a different port than 3000, the links in these instructions won't work.*
1. In your browser of choice, go to [https://localhost:3000](https://localhost:3000)
1. Click on "[Login](https://localhost:3000/users/sign_in)"
  1. Your credentials - which can be found in `./db/seeds.rb` - are:
    1. **Email:** orcid@sufia.org
    1. **Password:** icanhazorcid
    1. *Note: The email used to sign in to this application need not match any of the emails associated with an ORCiD.*
1. Edit your profile
  1. Click on your email in the top right corner
  1. Then click "[Edit your Profile](https://localhost:3000/users/orcid@sufia-dot-org/edit)"

You can now interact with the Orcid widget.
