# Passport.js authentication for Amigame

[Passport](http://passportjs.org/) strategy for authenticating with [Amigame](http://amigame.co/) using the OAuth 2.0 API.

This module lets you authenticate using Amigame in your Node.js applications.

By plugging into Passport, Amigame authentication can be easily and unobtrusively integrated into any application or framework that supports [Connect](http://www.senchalabs.org/connect/)-style middleware, including [Express](http://expressjs.com/).

## Install
```
npm install passport-amigame
```

## Usage

#### Configure Strategy

The Amigame authentication strategy authenticates users using an Amigame account and OAuth 2.0 tokens.  The strategy requires a `verify` callback, which accepts these credentials and calls `done` providing a user, as well as `options` specifying a client ID, client secret, and callback URL.
```
var OAuth2Strategy = require("passport-amigame").Strategy;

passport.use(new OAuth2Strategy({
	clientID: CLIENT_ID,
	clientSecret: CLIENT_SECRET,
	callbackURL: "http://www.example.net/auth/amigame/callback"
	},
	function(accessToken, refreshToken, profile, done) {
	User.findOrCreate({ providerId: profile.id }, function (err, user) {
		return done(err, user);
	});
	}
));
```

#### Authenticate Requests

Use `passport.authenticate()`, specifying the `'amigame'` strategy, to authenticate requests.

For example, as route middleware in an [Express](http://expressjs.com/) application:

```
app.get('/auth/amigame',
	passport.authenticate('amigame'));

app.get('/auth/amigame/callback',
	passport.authenticate('amigame', { failureRedirect: '/login' }),
	function(req, res) {
	// Successful authentication, redirect home.
	res.redirect('/');
	});
```

## Credits

Initiated by [Makis Tracend](http://github.com/tracend)

Part of [Amigame](http://amigame.co/) by [K&D Interactive](http://kdi.co/)

Released under the [MIT license](http://makesites.org/licenses/MIT)

