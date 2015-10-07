---
layout: post
title: "WebLogic server configuration with TLS"
date: 2015-10-05 12:57:49 -0700
comments: true
categories: [WLS, TLS, Chrome messes up WLS default SSL setting]
published: false
---

## Context
1.Chrome v45 and later forces the web server to support TLS certificate encryption. If not, the chrome will give you this error.

```
ERR_SSL_FALLBACK_BEYOND_MINIMUM_VERSION
```

2.Chrome also requires stronger encryption. The previous demo keystore used by WLS is not strong enough. The chrome will give you this error:

```
Server has a weak ephemeral Diffie-Hellman public key
```

3.



