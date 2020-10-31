# Heroku Buildpack for Crystal + Lucky Framework, with caching

This is a buildpack allowing easy and fast deployment of a [Lucky Framework](https://luckyframework.org) app to [Heroku](https://www.heroku.com/).

Forked from the [Lucky Framework Buildpack](https://github.com/luckyframework/heroku-buildpack-crystal) (which is itself a fork of the [Crystal Buildpack](https://github.com/crystal-lang/heroku-buildpack-crystal)).

This fork **dramatically increases deployment speed** due to the following enhancements:

- The Crystal installation is cached
- Shards are cached, and `shards install` is only run when `shard.yml` or `shard.lock` have changed
- Logging is improved to actually show what's happening in the slow process of installing shards and compiling the app

## Usage

Follow the [Lucky Framework Heroku deployment guide](https://luckyframework.org/guides/deploying/heroku), but instead of:

```bash
$ heroku buildpacks:add https://github.com/luckyframework/heroku-buildpack-crystal
```

run:

```bash
$ heroku buildpacks:add https://github.com/ZimbiX/heroku-buildpack-for-lucky-framework-with-caching
```

Note that this Buildpack is unofficial. If you're concerned about security (which you should be), you can fork this repo, read [the code](bin), and use your fork's URL instead of mine - to prevent any unwanted changes being automatically applied to your next deployment.

## Buildpack development

I haven't looked at the existing test suite enough, so I've been testing this using:

```bash
$ (cd ~/Projects/my-lucky-app && yarn && yarn prod) && ./bin/compile ~/Projects/my-lucky-app $PWD/test-cache $PWD/test-env
```

## Todo

- [ ] Split this buildpack in two - the vast majority of the code is for Crystal and not specific to Lucky
- [ ] Figure out what to do about the unit tests (`tests/run`), which were already failing when I forked
