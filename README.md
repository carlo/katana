# Katana


## Overview

Opinionated personal URL shortener which runs on [Heroku][1] and uses
[MyRedis][2] as a backend. Shortening is done through the fabulous
[Guillotine][3] engine and its Redis adapter.

If you set `HTTP_USER` and `HTTP_PASS` all methods except `GETs` require basic
authentication.

This fork (of the original
[github.com/mrtazz/katana](https://github.com/mrtazz/katana)) keeps the
filename extension and tacks it onto the short URL.  For example,
`http://example.com/pretty-long-url/image.gif` becomes
`http://my.tiny.domain/abcd.gif`.  I like this better.


## Usage

You can use it exactly as any other guillotine app:

    curl -X POST http://my.tiny.domain --user foo:bar -i -F"url=http://github.com" -F"code=gh"


## Features

- Authentication
- Custom [Tweetbot][7] compatible endpoint
- Gauges support (to come)


## Setup

    git clone git://github.com/carlo/katana.git
    cd katana
    heroku create
    heroku addons:add myredis
    heroku domains:add my.tiny.domain
    git push heroku master

    # for gauges support
    heroku config:add GAUGES_TOKEN="token"
    heroku config:add GAUGES_GAUGE="gauge"
    
    # for authentication
    heroku config:add HTTP_USER="theuser"
    heroku config:add HTTP_PASS="thepass"


### Tweetbot

There is a custom endpoint which is compatible with how tweetbot expects
custom URL shorteners to behave. Activate it by setting

    TWEETBOT_API=true

in your environment variables. After that you can add URLs with a `GET` to

    http://my.tiny.domain/api/create/?url=http://github.com

Keep in mind that this endpoint is not authenticated.


## Thanks

[@technoweenie][4] for the awesome guillotine and [@roidrage][5] for
[s3itch][6] which somehow got me started wanting a personal URL shortener.

[1]: http://heroku.com
[2]: https://myredis.com
[3]: https://github.com/technoweenie/guillotine
[4]: https://twitter.com/technoweenie
[5]: https://twitter.com/roidrage
[6]: https://github.com/mattmatt/s3itch
[7]: http://tapbots.com/software/tweetbot/
