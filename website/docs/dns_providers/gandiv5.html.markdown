---
layout: "acme"
page_title: "ACME: Gandi LiveDNS Challenge Provider"
sidebar_current: "docs-acme-dns-providers-v5-gandi"
description: |-
  Provides a resource to manage certificates on an ACME CA.
---

# Gandi LiveDNS Challenge Provider

The `gandiv5` DNS challenge provider can be used to perform DNS challenges for
the [`acme_certificate`][resource-acme-certificate] resource with
[Gandi LiveDNS][provider-service-page].

-> **NOTE:** For the legacy Gandi DNS service, use the use the [`gandi`][gandi]
provider.

[resource-acme-certificate]: /docs/providers/acme/r/certificate.html
[provider-service-page]: https://doc.livedns.gandi.net/
[gandi]: /docs/providers/acme/dns_providers/gandi.html

For complete information on how to use this provider with the `acme_certifiate`
resource, see [here][resource-acme-certificate-dns-challenges].

[resource-acme-certificate-dns-challenges]: /docs/providers/acme/r/certificate.html#using-dns-challenges

## Example

```hcl
resource "acme_certificate" "certificate" {
  ...

  dns_challenge {
    provider = "gandiv5"
  }
}
```

## Argument Reference

The following arguments can be either passed as environment variables, or
directly through the `config` block in the
[`dns_challenge`][resource-acme-certificate-dns-challenge-arg] argument in the
[`acme_certificate`][resource-acme-certificate] resource. For more details, see
[here][resource-acme-certificate-dns-challenges].

[resource-acme-certificate-dns-challenge-arg]: /docs/providers/acme/r/certificate.html#dns_challenge

* `GANDIV5_API_KEY` - The API key to use.

The following additional optional variables are available:

* `GANDIV5_POLLING_INTERVAL` - The amount of time, in seconds, to wait between
  DNS propagation checks (default: `20`).
* `GANDIV5_PROPAGATION_TIMEOUT` - The amount of time, in seconds, to wait for DNS
  propagation (default: `1200`).
* `GANDIV5_TTL` - The TTL to set on DNS challenge records, in seconds (default:
  `300`).
* `GANDIV5_HTTP_TIMEOUT` - The timeout on HTTP requests to the API (default:
  `10`).
