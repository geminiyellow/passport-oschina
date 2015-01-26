# passport-oschina

[Passport](http://passportjs.org/) strategy for authenticating with [OSChina](https://www.oschina.net/)
using the OAuth 2.0 API.

This module lets you authenticate using OSChina in your Node.js applications.
By plugging into Passport, OSChina authentication can be easily and
unobtrusively integrated into any application or framework that supports
[Connect](http://www.senchalabs.org/connect/)-style middleware, including
[Express](http://expressjs.com/).

## Install

    $ npm install passport-oschina

## Usage

#### Configure Strategy

The OSChina authentication strategy authenticates users using a OSChina account
and OAuth 2.0 tokens.  The strategy requires a `verify` callback, which accepts
these credentials and calls `done` providing a user, as well as `options`
specifying a client ID, client secret, and callback URL.

    passport.use(new OSChinaStrategy({
        clientID: OSCHINA_CLIENT_ID,
        clientSecret: OSCHINA_CLIENT_SECRET,
        callbackURL: "http://127.0.0.1:3000/auth/oschina/callback"
      },
      function(accessToken, refreshToken, profile, done) {
        User.findOrCreate({ oschinaId: profile.id }, function (err, user) {
          return done(err, user);
        });
      }
    ));

#### Authenticate Requests

Use `passport.authenticate()`, specifying the `'oschina'` strategy, to
authenticate requests.

For example, as route middleware in an [Express](http://expressjs.com/)
application:

    app.get('/auth/oschina',
      passport.authenticate('oschina'));

    app.get('/auth/oschina/callback', 
      passport.authenticate('oschina', { failureRedirect: '/login' }),
      function(req, res) {
        // Successful authentication, redirect home.
        res.redirect('/');
      });

## Credits

  - [geminiyellow](https://github.com/geminiyellow)

## License

[The MIT License](http://opensource.org/licenses/MIT)

