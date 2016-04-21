# Passport-Real-Debrid

[Passport](http://passportjs.org/) strategy for authenticating with [Trakt](http://trakt.tv/)
using the OAuth 2.0 API.

[![build status](https://img.shields.io/travis/alexperrault/passport-trakt.svg?style=flat-square)](http://travis-ci.org/alexperrault/passport-trakt)
[![coverage status](https://img.shields.io/coveralls/alexperrault/passport-trakt.svg?style=flat-square)](https://coveralls.io/r/alexperrault/passport-trakt)
[![quality](https://img.shields.io/codeclimate/github/alexperrault/passport-trakt.svg?style=flat-square)](https://codeclimate.com/github/alexperrault/passport-trakt)
[![npm version](https://img.shields.io/npm/v/passport-trakt.svg?style=flat-square)](https://www.npmjs.com/package/passport-trakt)
[![license](https://img.shields.io/npm/l/passport-trakt.svg?style=flat-square)](http://opensource.org/licenses/MIT)
[![dependency status](https://img.shields.io/david/alexperrault/passport-trakt.svg?style=flat-square)](https://www.npmjs.com/package/passport-trakt)
[![devDependency status](https://img.shields.io/david/dev/alexperrault/passport-trakt.svg?style=flat-square)](https://www.npmjs.com/package/passport-trakt)

[![npm install](https://nodei.co/npm/passport-trakt.png)](https://www.npmjs.com/package/passport-trakt)

This module lets you authenticate using Trakt in your Node.js applications.
By plugging into Passport, Trakt authentication can be easily and
unobtrusively integrated into any application or framework that supports
[Connect](http://www.senchalabs.org/connect/)-style middleware, including
[Express](http://expressjs.com/).

## Install

    $ npm install passport-trakt

## Usage

#### Configure Strategy

The Real-Debrid authentication strategy authenticates users using a Real-Debrid account
and OAuth 2.0 tokens.  The strategy requires a `verify` callback, which accepts
these credentials and calls `done` providing a user, as well as `options`
specifying a client ID, client secret, and callback URL.

    passport.use(new TraktStrategy({
        clientID: REAL_DEBRID_CLIENT_ID,
        clientSecret: REAL_DEBRID_CLIENT_SECRET,
        callbackURL: "https://127.0.0.1:3000/auth/real-debrid/callback"
      },
      function(accessToken, refreshToken, params, profile, done) {
        User.findOrCreate({ realDebridId: profile.id }, function (err, user) {
          return done(err, user);
        });
      }
    ));

#### Authenticate Requests

Use `passport.authenticate()`, specifying the `'real-debrid'` strategy, to
authenticate requests.

For example, as route middleware in an [Express](http://expressjs.com/)
application:

    app.get('/auth/real-debrid',
      passport.authenticate('real-debrid'));

    app.get('/auth/real-debrid/callback', 
      passport.authenticate('real-debrid', { failureRedirect: '/login' }),
      function(req, res) {
        // Successful authentication, redirect home.
        res.redirect('/');
      });

## Credits

  - [Paul Bottein](http://github.com/piitaya)

## License

[The MIT License](https://github.com/piitaya/passport-real-debrid/blob/master/LICENSE)

Copyright (c) 2016 Paul Bottein

