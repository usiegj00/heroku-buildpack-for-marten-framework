# Heroku Buildpack for Crystal + Marten Framework, with caching

This is a buildpack allowing easy and fast deployment of a [Marten Framework](https://martenframework.com/) app to [Heroku](https://www.heroku.com/).

Forked from the [Lucky Framework Buildpack With Caching](https://github.com/ZimbiX/heroku-buildpack-for-lucky-framework-with-caching) which forked the [Lucky Framework Buildpack](https://github.com/luckyframework/heroku-buildpack-crystal) (which is itself a fork of the [Crystal Buildpack](https://github.com/crystal-lang/heroku-buildpack-crystal)).

This fork works with Marten and keeps the other goodies:

- Crystal build cache is retained (normally at `~/.cache/crystal`)
- Shards are cached (`lib`)
- `shards install` is only run when `shard.yml` or `shard.lock` have changed
- Crystal version installation is cached
- Logging is improved to actually show what's happening in the slow process of installing shards and compiling the app

## Usage

```bash
$ heroku buildpacks:add https://github.com/usiegj00/heroku-buildpack-for-marten-framework
```

Note that this Buildpack is unofficial. If you're concerned about security (which you should be), you can fork this repo, read [the code](bin), and use your fork's URL instead of mine - to prevent any unwanted changes being automatically applied to your next deployment.

## Buildpack development

I haven't looked at the existing test suite enough, so I've been testing this using:

```bash
$ (cd ~/Projects/my-lucky-app && yarn && yarn prod) && ./bin/compile ~/Projects/my-lucky-app $PWD/test-cache $PWD/test-env
```
