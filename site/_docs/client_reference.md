---
layout: docs
title: Client Reference
sidebar_title: Client Reference
permalink: /docs/client_reference.html
---

<!--
{% comment %}
Licensed to the Apache Software Foundation (ASF) under one or more
contributor license agreements.  See the NOTICE file distributed with
this work for additional information regarding copyright ownership.
The ASF licenses this file to you under the Apache License, Version 2.0
(the "License"); you may not use this file except in compliance with
the License.  You may obtain a copy of the License at

http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
{% endcomment %}
-->

Avatica provides a reference-implementation client in the form of a Java
JDBC client that interacts with the Avatica server over HTTP. This client
can be used just as any other JDBC driver. There are a number of options
that are available for clients to specify via the JDBC connection URL.

As a reminder, the JDBC connection URL for Avatica is:

  `jdbc:avatica:remote:[option=value[;option=value]]`

The following are a list of supported options:

{% comment %}
It's a shame that we have to embed HTML to get the anchors but the normal
header tags from kramdown screw up the definition list. We lose the pretty
on-hover images for the permalink, but oh well.
{% endcomment %}

<strong><a name="url" href="#url">url</a></strong>

: _Description_: This property is a URL which refers to the location of the
  Avatica Server which the driver will communicate with.

: _Default_: This property's default value is `null`. It is required that the
  user provides a value for this property.

: _Required_: Yes.


<strong><a name="serialization" href="#serialization">serialization</a></strong>

: _Description_: Avatica supports multiple types of serialization mechanisms
  to format data between the client and server. This property is used to ensure
  that the client and server both use the same serialization mechanism. Valid
  values presently include `json` and `protobuf`.

: _Default_: `json` is the default value.

: _Required_: No.


<strong><a name="authentication" href="#authentication">authentication</a></strong>

: _Description_: Avatica clients can specify the means in which it authenticates
  with the Avatica server. Clients who want to use a specific form
  of authentication should specify the appropriate value in this property. Valid
  values for this property are presently: `NONE`, `BASIC`, `DIGEST`, and `SPNEGO`.

: _Default_: `null` (implying "no authentication", equivalent to `NONE`).

: _Required_: No.


<strong><a name="timeZone" href="#timeZone">timeZone</a></strong>

: _Description_: The timezone that will be used for dates and times. Valid values for this
  property are defined by [RFC 822](https://www.ietf.org/rfc/rfc0822.txt), for
  example: `GMT`, `GMT-3`, `EST` or `PDT`.

: _Default_: This property's default value is `null` which will cause the Avatica Driver to
  use the default timezone as specified by the JVM, commonly overriden by the
  `user.timezone` system property.

: _Required_: No.


<strong><a name="httpclient-factory" href="#httpclient-factory">httpclient_factory</a></strong>

: _Description_: The Avatica client is a "fancy" HTTP client. As such, there are
  many libraries and APIs available for making HTTP calls. To determine which implementation
  should be used, there is an interface `AvaticaHttpClientFactory` which can be provided
  to control how the `AvaticaHttpClient` implementation is chosen.

: _Default_: `AvaticaHttpClientFactoryImpl`.

: _Required_: No.


<strong><a name="httpclient-impl" href="#httpclient-impl">httpclient_impl</a></strong>

: _Description_: When using the default `AvaticaHttpClientFactoryImpl` HTTP client factory
  implementation, this factory should choose the correct client implementation for the
  given client configuration. This property can be used to override the specific HTTP
  client implementation. If it is not provided, the `AvaticaHttpClientFactoryImpl` will
  automatically choose the HTTP client implementation.

: _Default_: `null`.

: _Required_: No.

<strong><a name="avatica-user" href="#avatica-user">avatica_user</a></strong>

: _Description_: This is the username used by an Avatica client to identify itself
  to the Avatica server. It is unique to the traditional "user" JDBC property. It
  is only necessary if Avatica is configured for HTTP Basic or Digest authentication.

: _Default_: `null`.

: _Required_: No.

<strong><a name="avatica-password" href="#avatica-password">avatica_password</a></strong>

: _Description_: This is the password used by an Avatica client to identify itself
  to the Avatica server. It is unique to the traditional "password" JDBC property. It
  is only necessary if Avatica is configured for HTTP Basic or Digest authentication.

: _Default_: `null`.

: _Required_: No.

<strong><a name="principal" href="#principal">principal</a></strong>

: _Description_: The Kerberos principal which can be used by the Avatica JDBC Driver
  to automatically perform a Kerberos login before attempting to contact the Avatica
  server. If this property is provided, it is also expected that `keytab` is provided
  and that the Avatica server is configured for SPNEGO authentication. Users can perform
  their own Kerberos login; this option is provided only as a convenience.

: _Default_: `null`.

: _Required_: No.

<strong><a name="keytab" href="#keytab">keytab</a></strong>

: _Description_: The Kerberos keytab which contains the secret material to perform
  a Kerberos login with the `principal`. The value should be a path on the local
  filesystem to a regular file.

: _Default_: `null`.

: _Required_: No.

<strong><a name="truststore" href="#truststore">truststore</a></strong>

: _Description_: A path to a Java KeyStore (JKS) file on the local filesystem
  which contains the certificate authority to trust in a TLS handshake. Only
  necessary when using HTTPS.

: _Default_: `null`.

: _Required_: No.

<strong><a name="truststore_password" href="#truststore_password">truststore_password</a></strong>

: _Description_: The password for the Java KeyStore file specified by <a href="#truststore">truststore</a>.

: _Default_: `null`.

: _Required_: Only if `truststore` was provided.

<strong><a name="keystore_type" href="#keystore_type">keystore_type</a></strong>

: _Description_: The format of the truststore file specified by 
  <a href="#truststore">truststore</a>. This needs to be specified if non JKS format keystores are
  used (i.e. BCFKS). This setting applies both to keystore and truststore files.
  For formats not included in the default JVM the corresponding security provider must be installed
  and configured into the JVM, or added to the application classpath and configured.

: _Default_: `null`.

: _Required_: No.

<strong><a name="fetch_size" href="#fetch_size">fetch_size</a></strong>

: _Description_: The number of rows to fetch. If
    <a href="https://docs.oracle.com/javase/8/docs/api/java/sql/Statement.html#setFetchSize-int-">
    Statement:setFetchSize</a> is set, that value overrides fetch_size.

: _Default_: `100`.

: _Required_: No.

<strong><a name="transparent_reconnection" href="#transparent_reconnection">transparent_reconnection</a></strong>

: _Description_: The Java client versions between 1.5.0 and 1.20.0 transparently re-created
  the Connection object on the client side if it expired from the server cache. This behaviour broke
  JDBC compliance and could cause data loss for transactional write workloads, and has been removed
  in 1.21.0. Setting this property to `true` restores the 1.20.0 behaviour.

: _Default_: `false`.

: _Required_: No.

<strong><a name="use_client_side_lb" href="#use_client_side_lb">use_client_side_lb</a></strong>

: _Description_: Enables the client side load-balancing.

: _Default_: `false`.

: _Required_: No.

<strong><a name="lb_urls" href="#lb_urls">lb_urls</a></strong>

: _Description_: List of URLs in a comma separated format, for example "URL1,URL2...URLn", to be used by the client side
load balancer. Depending on the load balancing strategy, load balancer selects one of the URLs from the list.

: _Default_: `null`.

: _Required_: No.

<strong><a name="lb_strategy" href="#lb_strategy">lb_strategy</a></strong>

: _Description_: The load balancing strategy to be used by the client side load balancer. It must be a fully qualified
Java class name which implements `org.apache.calcite.avatica.ha.LBStrategy`. Three implementations are provided
`org.apache.calcite.avatica.ha.RandomSelectLBStrategy`, `org.apache.calcite.avatica.ha.RoundRobinLBStrategy` and
`org.apache.calcite.avatica.ha.ShuffledRoundRobinLBStrategy`

: _Default_: `org.apache.calcite.avatica.ha.ShuffledRoundRobinLBStrategy`.

: _Required_: No.

<strong><a name="lb_connection_failover_retries" href="#lb_connection_failover_retries">lb_connection_failover_retries</a></strong>

: _Description_: Number of times that the load balancer tries to retry the connection with another URL (fail-over).
When the connection fails, load balancer retries the connection with another URL, chosen by the load balancing strategy.

: _Default_: `3`.

: _Required_: No.

<strong><a name="lb_connection_failover_sleep_time" href="#lb_connection_failover_sleep_time">lb_connection_failover_sleep_time</a></strong>

: _Description_: The amount of time in milliseconds that the load balancer sleeps before attempting the next connection
failover retry.

: _Default_: `1000`.

: _Required_: No.

<strong><a name="http_connection_timeout" href="#http_connection_timeout">http_connection_timeout</a></strong>

: _Description_: Timeout in milliseconds for the connection between the Avatica HTTP client and server.

: _Default_: `180000` (3 minutes).

: _Required_: No.
