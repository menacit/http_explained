---
SPDX-FileCopyrightText: © 2026 Menacit AB <foss@menacit.se>
SPDX-License-Identifier: CC-BY-SA-4.0

title: "HTTP explained"
author: "Joel Rangsmo <joel@menacit.se>"
footer: "© Course authors (CC BY-SA 4.0)"
description: "Introduction to wonderful world of HTTP"
keywords:
  - "http"
  - "https"
  - "tls"
  - "x509"
color: "#ffffff"
class:
  - "invert"
style: |
  section.center {
    text-align: center;
  }

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Pedro Mendes (CC BY-SA 2.0)" -->
# HTTP(S) explained
### A ~~somewhat gentle~~ introduction

![bg right:30%](images/arecibo.jpg)

<!--
Welcome participants and wait for everyone to get settled.
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Pedro Mendes (CC BY-SA 2.0)" -->
Our modern  world runs on the
**H**yper**t**ext **T**ransfer **P**rotocol,
but how does it really work?  
  
Why is HTTP**S** a thing?  

Where do "proxies"
and "load balancers"
come into the picture?  

After this presentation,
you should feel comfortable 
answering these questions! :-D

![bg right:30%](images/arecibo.jpg)

<!--
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Kuhnmi (CC BY 2.0)" -->
## Brief history
(Relatively) simple protocol for
client (_AKA "user agent"_) to
server communication.  

Introduced together with HTML in
1989 to serve files over the network.  

Three major protocol versions exist,
with the latest being release in 2022.

![bg right:30%](images/kolibri.jpg)

<!--
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Marcin Wichary (CC BY 2.0)" -->
## The early days
Basic serving of static files.  

A client request for
**http://example.com/animals/horse.html**
would simply load the contents of
**/var/www/html/animals/horse.html**
from the server's file system
and transfer it to the client.

![bg right:30%](images/90s_tv.jpg)

<!--
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% ETC Project (CC0 1.0)" -->
## Things getting fancier
People wanted to use the web
to provide interactive applications,
such as online shopping malls.  

Lowered the bar for adoption significantly,
as users didn't have to install/update
additional software on their computers.

Instead of just serving static files
from disk, the server would generate
dynamic responses on-the-fly.  

![bg right:30%](images/computer_man.jpg)

<!--
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% ETC Project (CC0 1.0)" -->
A client request for
**http://example.com/weather.cgi?city=Gnarp**
may resulted in the following response
being generated and return by the server:

```html
<html>
  <head>
    <title>Weather now in Gnarp</title>
  </head>
  <body>
    <p>
      The current (19:06) temperature
      in <b>Gnarp</b> is
      19 degrees celsius.<br>
      It is raining! :-(
    </p>
  </body>
</html>
```

![bg right:30%](images/computer_man.jpg)

<!--
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Price Capsule (CC BY-SA 2.0)" -->
## Becoming Esperanto
These days HTTP isn't only used to
serve HTML data to web browsers,
but for a wide variety of
client-server communication needs.  

Liked by developers for its
simplicity and widespread support
in programming languages/toolkits.

![bg right:30%](images/desert_hut.jpg)

<!--
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Pedro Ribeiro Simões (CC BY 2.0)" -->
If it's so damn simple,
can't you just get to it?!  
  
Waow, chill - I shall!  
  
Just one more thing...

![bg right:30%](images/street_art_man.jpg)

<!--
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Marcin Wichary (CC BY 2.0)" -->
## Defining URLs
Applications are typically given
**U**niform **R**esource **L**ocators
to known where they should send requests.  

**http://www.example.com/cocktails.txt**
tells the client to use the HTTP protocol,
connect to the host address "www.example.com"
and request the server path "/cocktails.txt".  

![bg right:30%](images/train_track.jpg)

<!--
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Nicholas A. Tonelli (CC0 1.0)" -->
## Not only for HTTP
**irc://chat.example.com/the\_corner\_bar**
tells the client to use the
**I**nternet **R**elay **C**hat protocol,
connect to the host address "chat.example.com"
and join a chat room named "the\_corner\_bar".

Not so complicated, right?

![bg right:30%](images/forest_road.jpg)

<!--
-->


---
<!-- _footer: "%ATTRIBUTION_PREFIX% Jan Hrdina (CC BY-SA 2.0)" -->
httpː//bob:s3cret@t.example.com:1234 ↴
/about+us/faq?lan=en&s=Q%26A#q:Refund

![bg right:30%](images/optics.jpg)

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Jan Hrdina (CC BY-SA 2.0)" -->
## Breaking down a URL
**http**ː//bob:s3cret@t.example.com:1234 ↴
/about+us/faq?lan=en&s=Q%26A#q:Refund

```
Protocol, also known as "scheme".

Commonly "http" or "https".





```

![bg right:30%](images/optics.jpg)

<!--
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Jan Hrdina (CC BY-SA 2.0)" -->
## Breaking down a URL
httpː//**bob:s3cret**@t.example.com:1234 ↴
/about+us/faq?lan=en&s=Q%26A#q:Refund

```
Optional username and password for
authentication, separated by colon.

May be omitted and not considered
best-practice.



```

![bg right:30%](images/optics.jpg)

<!--
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Jan Hrdina (CC BY-SA 2.0)" -->
## Breaking down a URL
httpː//bob:s3cret@**t.example.com**:1234 ↴
/about+us/faq?lan=en&s=Q%26A#q:Refund

```
Target server network address.

Either host name, commonly resolved
by client using DNS, or IP address.




```

![bg right:30%](images/optics.jpg)

<!--
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Jan Hrdina (CC BY-SA 2.0)" -->
## Breaking down a URL
httpː//bob:s3cret@t.example.com:**1234** ↴
/about+us/faq?lan=en&s=Q%26A#q:Refund

```
Target port for connection to server.
If ommited, the default port is used:

HTTP version 1 and 2: 80/TCP 
HTTPS: 443/TCP
HTTP version 3: 443/UDP


```

![bg right:30%](images/optics.jpg)

<!--
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Jan Hrdina (CC BY-SA 2.0)" -->
## Breaking down a URL
httpː//bob:s3cret@t.example.com:1234 ↴
**/about+us/faq?lan=en&s=Q%26A#q:Refund**

```
Data path that client should request*
from the server.

The plus character is converted to space.
Other characters with special meaning in
URL path may be "percentage encoded":

%20 = Space, %2F = /, %26 = &, %25 = %...
```

![bg right:30%](images/optics.jpg)

<!--
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Yellowcloud (CC BY 2.0)" -->
## Breaking down a URL path
httpː//bob:s3cret@t.example.com:1234 ↴
**/about+us/faq**?lan=en&s=Q%26A#q:Refund

```
Base path.

Similar to a file system path.

Doesn't require file extension,
like ".html" or ".jpeg", other methods
exist for communicating response format.

```

![bg right:30%](images/chip_closeup.jpg)

<!--
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Yellowcloud (CC BY 2.0)" -->
## Breaking down a URL path
httpː//bob:s3cret@t.example.com:1234 ↴
/about+us/faq?**lan=en&s=Q%26A**#q:Refund

```
Optional "query string".

Key-value pairs, separated by
ampersand (or less commonly semicolon).

Commonly used to pass data to server
as input for generation of
dynamic responses.
```

![bg right:30%](images/chip_closeup.jpg)

<!--
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Yellowcloud (CC BY 2.0)" -->
## Breaking down a URL path
httpː//bob:s3cret@t.example.com:1234 ↴
/about+us/faq?lan=en&s=Q%26A#**q:Refund**

```
Optional "fragment".

Part of the URL that is never actually
in requests to the server, but may be 
interpreted by the client application.

Commonly used for high-lighting text,
passing client-side secrets, etc.
```

![bg right:30%](images/chip_closeup.jpg)

<!--
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Theo Crazzolara (CC BY 2.0)" -->
## URL parsing woes
Properly (and consistently) grokking
URLs seems tricky for both
humans and computers.

Where will we end up using
**httpː//chat.fb.com:1814/start.php@test.io** ,
**httpː//googIe.com** or
**httpː//facebοοk.com** ?

Loosely defined/interpreted standards
have resulted in many security issues.

![bg right:30%](images/sad_bird.jpg)

<!--
-->

---
![bg center 65%](images/emoji_domain.png)

<!--
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Mario Hoppmann (CC BY 2.0)" -->
With that out of the way,
let's examine the
HTTP protocol!

![bg right:30%](images/polar_bear.jpg)

<!--
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Jason Thibault (CC BY 2.0)" -->
## The basics
HTTP version 1 is a
text-based protocol.

Makes it simple to learn,
debug and implement.  

A **request** is sent by
the client, resulting in
a **response** being
returned by the server.

![bg right:30%](images/habitat_67.jpg)

<!--
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Torkild Retvedt (CC BY-SA 2.0)" -->
## HTTP v1.1 request
```
<METHOD> <PATH> HTTP/1.1
Host: <TARGET HOST NAME OR IP ADDRESS>
<OPTIONAL HEADER NAME>: <HEADER VALUE>

<OPTIONAL BODY>
```

![bg right:30%](images/cameleon.jpg)

<!--
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Jesse James (CC BY 2.0)" -->
## Very basic request
```
GET /cocktails.txt HTTP/1.1
Host: www.example.com

```

![bg right:30%](images/party.jpg)

<!--
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Jesse James (CC BY 2.0)" -->
## Another simple example
```
DELETE /api/user/42 HTTP/1.1
Host: management.example.com
Authorization: Basic Ym9iOnMzY3JldA==

```

_Ym9iOnMzY3JldA== is
"bob:s3cret" encoded
using Base64._

![bg right:30%](images/man_statue.jpg)

<!--
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Fredrik Rubensson (CC BY-SA 2.0)" -->
## Including data in body
```
POST /guest_book.php HTTP/1.1
Host: social.example.com
Content-Type: application/json
Content-Length: 51

{
  "author": "adam",
  "message": "Hello Eve!!!"
}
```

![bg right:30%](images/log_on_log.jpg)

<!--
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Fredrik Rubensson (CC BY-SA 2.0)" -->
## HTTP v1.1 response
```
HTTP/1.1 <STATUS CODE> <STATUS MESSAGE>
<OPTIONAL HEADER NAME>: <HEADER VALUE>

<OPTIONAL BODY>
```

![bg right:30%](images/astronaut_streetart.jpg)

<!--
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Pyntofmyld (CC BY 2.0)" -->
## Very basic response
```
HTTP/1.1 204

```


![bg right:30%](images/pdp11.jpg)

<!--
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Marcin Wichary (CC BY 2.0)" -->
## Status code categories
- Informational (100 – 199)
- Successful (200 – 299)
- Redirection (300 – 399)
- Client error (400 – 499)
- Server error (500 – 599)

![bg right:30%](images/numbers_pad.jpg)

<!--
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Marcin Wichary (CC BY 2.0)" -->
## Common status codes
- **200**: Informational: OK
- **204**: Informational: No content
- **301**: Redirection: Moved permanently
- **400**: Client error: Bad request
- **401**: Client error: Unauthorized
- **404**: Client error: Not found
- **500**: Server error: Internal server error
- **503**: Server error: Bad gateway

![bg right:30%](images/numbers_pad.jpg)

<!--
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Marcin Wichary (CC BY 2.0)" -->
...and of course **418**:

> The HTTP 418 ("I'm a teapot")
> status response code indicates
> that the server refuses to brew coffee
> because it is, permanently, a teapot.

— _MDN web docs_

![bg right:30%](images/numbers_pad.jpg)

<!--
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Martin Fisch (CC BY 2.0)" -->
## Another simple example
```
HTTP/1.1 500 Wooops
X-Server: Example HTTPD v0.2

```

![bg right:30%](images/fire.jpg)

<!--
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Scott Schiller (CC BY 2.0)" -->
## Including data in body
```
HTTP/1.1 200 OK
Content-Type: text/plain
Content-Length: 67

Top three coctails:

1. Caipirinha
2. White Russian
3. Bloody Mary
```

![bg right:30%](images/pcb.jpg)

<!--
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Jeena Paradies (CC BY 2.0)" -->
Doesn't seem too tricky.  

Let's hack together our own
client and server using
**Netcat**!

![bg right:30%](images/lion_statue.jpg)

<!--
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Sergei F (CC BY 2.0)" -->
## The S in HTTPS
HTTP is a "clear-text" protocol.  

Communication can be intercepted
(and modified) anywhere between
the server and the client.  

HTTPS was created to wrap HTTP
in a layer of encryption.  

Relies on both symmetric and
asymmetric cryptography.  

Let's jump into Menacit's
["Practical cryptography course"](https://t.menacit.se/crypto)!

![bg right:30%](images/rusty_lock.jpg)

<!--
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Stig Nygaard (CC BY 2.0)" -->
## HTTP proxies
An HTTP proxy is a piece of
software acting as both a
server and a client at
the same time.

Can be used to filter,
redirect and manipulate
HTTP requests from clients.  

![bg right:30%](images/holmen_crane.jpg)

<!--
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Brendan J (CC BY 2.0)" -->
## Forward proxies
Commonly used to restrict
egress communication on a network
or provide some client anonymity.

> A HTTP request reaches the forward proxy.
> If the host header contains "example.com",
> the proxy sends a HTTP request to
> "example.com" and returns its
> response to the client.

_(may log requests, return status code 403
for disallowed host names and similar)_

![bg right:30%](images/gate.jpg)

<!--
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Austin Design (CC BY-SA 2.0)" -->
## Reverse proxies
Commonly used to restrict or redirect client
requests (ingress) to another HTTP server.

> A HTTP request reaches the reverse proxy.
>
> If the URL path begins with "/contact",
> the reverse proxy sends a HTTP request
> to "w1.int.example.com" and returns
> its response to the client.
>
> Otherwise, the reverse proxy sends a
> HTTP request to "w2.int.example.com"
> and returns its response to the client.

![bg right:30%](images/noise_tower.jpg)

<!--
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Rod Waddington (CC BY-SA 2.0)" -->
## Load balancers
Forwards traffic to multiple servers,
distributing the load.  

Can monitor status of servers and
exclude them as targets if they
become unhealthy.

All\* HTTP load balancers are
reverse proxies, but not all
reverse proxies are load balancers.

![bg right:30%](images/green_cabling.jpg)

<!--
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Rod Waddington (CC BY-SA 2.0)" -->
> A HTTP request reaches the load balancer.
> 
> If the host header contains "example.com",
> the load balancer sends a HTTP request to
> either "w1.example.com" or "w2.example.com"
> (depending on their load/availability)
> and returns its response to the client.

![bg right:30%](images/green_cabling.jpg)

<!--
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Adam Lusch (CC BY-SA 2.0)" -->
What happened after HTTP version 1.1?

![bg right:30%](images/demolition_pigeon.jpg)

<!--
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Thierry Ehrmann (CC BY 2.0)" -->
## HTTP version 2
Introduced back in 2015,
first major change since 1997.  

Still uses the same verbs, status codes,
header/body concepts - but no longer a
simple text based protocol.

Features like multi-plexing, server-side push
and header compression provides better
performance/lower latency.

Huge resource savings for
large web-site operators.

![bg right:30%](images/wireframe.jpg)

<!--
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% David Revoy (CC BY 3.0)" -->
## HTTP version 3
Standardized in 2022,
support still being implemented
in client/server/proxy software.

Abandons TCP in favor of the
UDP-based transport protocol "QUIC".

Mandatory TLS-like encryption and
further performance improvements.

![bg right:30%](images/cyberpunk.jpg)

<!--
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Nirvana Studios (CC BY 4.0)" -->
We haven't yet talked about cookies,
WebSockets and other exciting things!

...but that's a story for another day.

![bg right:30%](images/installation_the_singularity.jpg)

<!--
-->

---
For copy-pasteable
speaker notes, example code
and similar goodies, see:   
**[%RESOURCES_DOMAIN%/http.zip](%RESOURCES_ARCHIVE%)**.  

![bg right 90%](qr_codes/presentation_zip.link.svg)

<!--
- Speaker notes in slides are heavily recommended for recaps/deep diving
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Amy Nelson (CC BY 3.0)" -->
## Thanks for listening!
Was anything unclear?  
Got ideas for improvements?  
Don't fancy the animals in the slides?  
  
Create an issue or submit a pull request to
[the repository on Github](https://github.com/menacit/http_explained)!

![bg right:30%](images/lizard.jpg)

<!--
- Encourage participants to make the presentation better

- Learners are likely the best to provide critique, lecturers are likely a bit home-blind

- No cats or dogs allowed!

- Feel free to share it with friends or use it yourself later in your career
-->
