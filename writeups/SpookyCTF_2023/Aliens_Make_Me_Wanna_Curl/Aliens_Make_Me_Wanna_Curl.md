# Aliens Make Me Wanna Curl
Writeup Author: nazareth
## Description
* Author: Exiden
* Category: web

We are expecting communications from an artificial intelligence device called MU-TH-UR 6000, referred to as mother by the crew. We disabled the login page and implemented a different method of authentication. The username is mother and the password is ovomorph. To ensure security, only mothers specific browser is allowed.

https://spooky-aliens-make-me-wanna-curl-web.chals.io/flag

## Writeup
The first thing I tried was navigating to the url via Firefox. The page displays this text:
![Alt text](image-4.png)

So, because the name of the challenge has the word `curl` in it, I assumed I would need to use the `curl` command in order to access the url and authenticate.

As a sanity check, I ran the following to make sure the page returned was the same...and it was:
```
$ curl https://spooky-aliens-make-me-wanna-curl-web.chals.io/flag

No auth!
```

Next, I looked for a `curl` option that would allow me to authenticate with the username and password found in the challenge description: `mother` and `ovomorph`.

The `--user` option enables this. So, I ran the following and got a different result:
```
$ curl --user mother:ovomorph https://spooky-aliens-make-me-wanna-curl-web.chals.io/flag

Incorrect Device!
```

Finally, I noticed the challenge description says "only mothers specific browser is allowed." I assumed this hint and the `Incorrect Device!` output were referring to the same thing: changing the User-Agent header.

I searched for an option with `curl` where I could set the User-Agent header and found the `-A` option.

Then, I needed to figure out what to set the User-Agent header to. Looking back at the challenge description, it mentions a "device called MU-TH-UR 6000" which is what it's expecting communications from. So, I ran the following command, and it printed the flag!

```
curl --user mother:ovomorph -A "MU-TH-UR 6000" https://spooky-aliens-make-me-wanna-curl-web.chals.io/flag
```

Flag: `NICC{dOnt_d3pEnD_On_h3AdeRs_4_s3eCu1ty}`