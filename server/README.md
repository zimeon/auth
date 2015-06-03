# IIIF test server with authentication

## Setup

Set up Google credentials at <https://developers.google.com/identity/protocols/OpenIDConnect>. Want to sign up for a web application and must set the origin and redirect URIs. The redirect URI is `BASEPREF+/home` on the auth servers. From the "Credentials" page use "Download JSON" and save this file as `client_secret.json` in this directory.

## Runnning

The script `run_server_localhost_8001.sh` first cleans out the webcache (there are no checks for currency so a change in the code will not cause cache expiry!) and then runs `pi3f.oauth.py`. Currently all the config is in `pi3f.oauth.py` and the Google API secret assumed to be in `client_secret.json`.

```
simeon@Cider server>./run_server_localhost_8001.sh 
Running with HOMEDIR = /Users/simeon/iiif/auth/server
Bottle v0.12.8 server starting up (using WSGIRefServer())...
Listening on http://localhost:8001/
Hit Ctrl-C to quit.
```

access to <http://localhost:8001/> gives `An error occured when processing the 'identifier' parameter:  Identifier invalid: ''` and the log:

```
127.0.0.1 - - [03/Jun/2015 13:30:22] "GET / HTTP/1.1" 400 84
```

access to <http://localhost:8001/tetons> redirects to info.json and then to degraded:

```
127.0.0.1 - - [03/Jun/2015 13:33:10] "GET /tetons HTTP/1.1" 303 0
127.0.0.1 - - [03/Jun/2015 13:33:10] "GET /tetons/info.json HTTP/1.1" 303 0
127.0.0.1 - - [03/Jun/2015 13:33:10] "GET /tetons-degraded/info.json HTTP/1.1" 200 1086
```

access to <http://localhost:8001/tetons-degraded/full/full/0/default.jpg> gives the full degraded image:

```
127.0.0.1 - - [03/Jun/2015 13:34:22] "GET /tetons-degraded/full/full/0/default.jpg HTTP/1.1" 200 34162
```

See notes in /client/osd in this repo for client using this auth server.
