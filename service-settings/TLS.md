---
lastmod: 2019-02-22
date: 2019-02-22
linktitle: TLS
title: Enabling TLS for HTTPS and HTTP/2
weight: 10
menu:
  community_current:
    parent: "030 Service Settings"
---
There are two different strategies when using TLS over KrakenD:

- Use TLS for HTTPS and HTTP/2 in KrakenD
- Use a balancer with TLS termination in front of KrakenD (e.g., ELB, HAproxy)

In case you want to enable TLS in KrakenD you need to add a `tls` key at service level (configuration's file root) with at least the public key and the private key. When you add TLS, KrakenD listens **only using TLS**, and no traffic to plain HTTP is accepted.

## Simple configuration for TLS
To start KrakenD with TLS you need to generate the certificate and provide both the public and the private key:

    {
      "version": 2,
      "tls": {
        "public_key": "/path/to/cert.pem",
        "private_key": "/path/to/key.pem"
      }
    }

## Full configuration for TLS
All the accepted options of the TLS configuration are:


- `public_key`: Absolute path to the public key, or relative to the current working directory (CWD)
- `private_key`: Absolute path to the private key, or relative to the current working directory (CWD)

Plus these optional:

- `disabled` (boolean): A temporary flag to disable TLS (e.g: while in development)
- `min_version` (string): Minimum TLS version (one of `SSL3.0`, `TLS10`, `TLS11` or `TLS12`)
- `max_version` (string): Maximum TLS version (one of `SSL3.0`, `TLS10`, `TLS11` or `TLS12`)
- `curve_preferences` (integer array): The list of all the identifiers for the curve preferences (use `23` for CurveP256, `24` for CurveP384 or `25` for CurveP521)
- `prefer_server_cipher_suites` (boolean): Enforces the use of one of the cipher suites offered by the server, instead of going with the suite proposed by the client.
- `cipher_suites` (integer array): The list of cipher suites (see below).
The list of cipher suites with its values is:

  - `5`: TLS_RSA_WITH_RC4_128_SHA
  - `10`: TLS_RSA_WITH_3DES_EDE_CBC_SHA
  - `47`: TLS_RSA_WITH_AES_128_CBC_SHA
  - `53`: TLS_RSA_WITH_AES_256_CBC_SHA
  - `60`: TLS_RSA_WITH_AES_128_CBC_SHA256
  - `156`: TLS_RSA_WITH_AES_128_GCM_SHA256
  - `157`: TLS_RSA_WITH_AES_256_GCM_SHA384
  - `49159`: TLS_ECDHE_ECDSA_WITH_RC4_128_SHA
  - `49161`: TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA
  - `49162`: TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA
  - `49169`: TLS_ECDHE_RSA_WITH_RC4_128_SHA
  - `49170`: TLS_ECDHE_RSA_WITH_3DES_EDE_CBC_SHA
  - `49171`: TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA
  - `49172`: TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA
  - `49187`: TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256
  - `49191`: TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256
  - `49199`: TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256
  - `49195`: TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256
  - `49200`: TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384
  - `49196`: TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384
  - `52392`: TLS_ECDHE_RSA_WITH_CHACHA20_POLY1305
  - `52393`: TLS_ECDHE_ECDSA_WITH_CHACHA20_POLY1305
