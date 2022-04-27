# DANE: TLSA DNS-record
## Generates a DNS TLSA-record for DANE / [RFC6698](https://datatracker.ietf.org/doc/html/rfc6698)

Bash script to print the suggested TLSA-record.

### Quick start:

```bash
$ bash dane-tlsa.sh "/path/to/cert.pem" 0 SHA256
```

### Syntax:

```bash
dane-tlsa.sh "/path/to/cert.pem" 0|1 [ SHA256|SHA512 ]
```

The first parameter defines the selector. Either uses the full certificate (0) or the public key (1).
<br>Using the full certificate (0) is advised (most secure).

The second parameter defines the hashing algorithm.
<br>When undefined, no hashing is done (exact match).

<hr />

### Considerations:

<hr />

#### Use the full certificate unless you have considered: [rfc6698#appendix-A.1.2.2](https://datatracker.ietf.org/doc/html/rfc6698#appendix-A.1.2.2)
> ... Unless the full implications of such an association are
> understood by the administrator, using selector type 0 is a better
> option from a security perspective.

<hr />

#### Use hashing for the full certificate. Without, the value can be too long.
In the case of selector 1 (public key): Not hashing can be considered.

<hr />

#### Use the same signature algorithm of your certificate: [rfc6698#section-2.1.3](https://datatracker.ietf.org/doc/html/rfc6698#section-2.1.3)
> If the TLSA record's matching type is a hash, having the record use
> the same hash algorithm that was used in the signature in the
> certificate (if possible) will assist clients that support a small
> number of hash algorithms.

<hr />

#### Use a low TTL to mitigate downtime when your certificate expires.
On a certificate renewal, the TLSA record could require an update.

<hr />

#### Use DANE-TA or DANE-EE with DNSSEC.
> ... but for the particular case of email communications we have the RFC7672, which describes the application of DANE and DNSSEC to communications (SMTP) between MTAs. In particular the RFC7672 recommends to use DANE-TA or DANE-EE with DNSSEC.

https://mecsa.jrc.ec.europa.eu/en/technical#dane

> ... With PKIX-TA(0) and PKIX-EE(1), the
   validation of peer certificate chains requires additional
   preconfigured CA TAs that are mutually trusted by the operators of
   the TLS server and client.

https://datatracker.ietf.org/doc/html/rfc7671#section-4

<hr />
