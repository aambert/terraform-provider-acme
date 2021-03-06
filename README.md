Terraform ACME Provider
========================

This is the repository for the Terraform ACME Provider, which one can use with
Terraform to manage and generate certificates generated by an [ACME][about-acme]
CA, such as [Let's Encrypt][lets-encrypt].

[about-acme]: https://ietf-wg-acme.github.io/acme/draft-ietf-acme-acme.html
[lets-encrypt]: https://letsencrypt.org

For general information about Terraform, visit the [official
website][terraform-io] and the [GitHub project page][terraform-gh].

[terraform-io]: https://www.terraform.io/
[terraform-gh]: https://github.com/hashicorp/terraform

:warning: **NOTE:** The ACME provider found here supports ACME v2 only.
For ACME v1 endpoints, version 0.6.0 is required, which can be found
[here][release-v0.6.0].

[release-v0.6.0]: https://github.com/vancluever/terraform-provider-acme/releases/tag/v0.6.0

# Using the Provider

The current version of this provider requires Terraform v0.10.2 or higher to
run.

Note that you need to run `terraform init` to fetch the provider before
deploying. Read about the provider split and other changes to TF v0.10.0 in the
official release announcement found [here][tf-0.10-announce].

[tf-0.10-announce]: https://www.hashicorp.com/blog/hashicorp-terraform-0-10/

## Full Provider Documentation

The provider is documented in full on the Terraform website and can be found
[here][tf-acme-docs].

[tf-acme-docs]: https://www.terraform.io/docs/providers/acme/index.html

### Controlling the provider version

Note that you can also control the provider version. This requires the use of a
`provider` block in your Terraform configuration if you have not added one
already.

The syntax is as follows:

```hcl
provider "acme" {
  version = "~> 1.0"
  ...
}
```

Version locking uses a pessimistic operator, so this version lock would mean
anything within the 1.x namespace, including or after 1.0.0. [Read
more][provider-vc] on provider version control.

[provider-vc]: https://www.terraform.io/docs/configuration/providers.html#provider-versions

# Building The Provider

**NOTE:** Unless you are [developing](#developing-the-provider) or require a
pre-release bugfix or feature, you will want to use the officially released
version of the provider (see [the section above](#using-the-provider)).

## Cloning the Project

```sh
git clone git@github.com:terraform-providers/terraform-provider-acme
```

## Running the Build

After the clone has been completed, you can enter the provider directory and
build the provider.

```sh
cd terraform-provider-acme
make build
```

## Installing the Local Plugin

After the build is complete, copy the `terraform-provider-acme` binary into
the same path as your `terraform` binary, and re-run `terraform init`.

After this, your project-local `.terraform/plugins/ARCH/lock.json` (where `ARCH`
matches the architecture of your machine) file should contain a SHA256 sum that
matches the local plugin. Run `shasum -a 256` on the binary to verify the values
match.

# Developing the Provider

**NOTE:** Before you start work on a feature, please make sure to check the
[issue tracker][gh-issues] and existing [pull requests][gh-prs] to ensure that
work is not being duplicated. For further clarification, you can also ask in a
new issue.

[gh-issues]: https://github.com/terraform-providers/terraform-provider-acme/issues
[gh-prs]: https://github.com/terraform-providers/terraform-provider-acme/pulls

If you wish to work on the provider, you'll first need [Go][go-website]
installed on your machine (version 1.11+ is **required**).

:warning: This provider uses [modules][go-modules]. Although a `vendor/`
directory is currently included with this project for backwards compatibility,
it may be removed at a later time. If you have trouble building the project in a
GOPATH, move the project outside of it.

[go-website]: https://golang.org/
[gopath]: http://golang.org/doc/code.html#GOPATH
[go-modules]: https://github.com/golang/go/wiki/Modules

See [Building the Provider](#building-the-provider) for details on building the provider.

# Testing the Provider

Testing the provider requires:

* An email address and valid domain name on AWS Route 53. These need to be set
using the `ACME_EMAIL_ADDRESS` and `ACME_CERT_DOMAIN` environment variables.
* Valid AWS credentials set in the environment - at the very least
`AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY`.

Some environment variables may be needed for other acceptance tests.

After this is done, you can run the acceptance tests by running:

```sh
$ make testacc
```

If you want to run against a specific set of tests, run `make testacc` with the
`TESTARGS` parameter containing the run mask as per below:

```sh
make testacc TESTARGS="-run=TestAccACMECertificate"
```

This following example would run all of the acceptance tests matching
`TestAccACMECertificate`. Change this for the specific tests you want to
run.

## License

```
Copyright 2018 Chris Marchesi
Copyright 2016-2018 PayByPhone Technologies, Inc.

This Source Code Form is subject to the terms of the Mozilla Public
License, v. 2.0. If a copy of the MPL was not distributed with this
file, You can obtain one at http://mozilla.org/MPL/2.0/.
 ```
