# Passport

## Config

Passport uses what are termed _strategies_ to authenticate requests. Strategies range from verifying a username and password, delegated authentication using [OAuth](http://oauth.net) or federated authentication using [OpenID](http://openid.net).

A strategy takes configuration options and a `verify` callback.

```typescript
const options = {
  usernameField: "uname",
  passwordField: "pw",
};

passport.use(new LocalStrategy(options, async (username: string, password: string, done: any) => {

  try {
    const user = await database<User>(tableNames.user)
      .where("username", username)
      .first();

    if (!user) {
      console.warn("User not found.");
      return done(null, false, { message: "User not found." });
    }

    const isValid = validPassword(password, user.hash, user.salt);

    if (isValid) {
      console.info(`Successfully logged in as ${user.username}`);
      return done(null, user, { message: `Successfully logged in as ${user.username}` });
    } else {
      console.warn("Password incorrect");
      return done(null, false, { message: "Password incorrect" });
    }
  } catch (error) {
    done(error);
  }
}));
```

## Initialisation

Before use the instance of passport which has been configured needs to be initialised and added into the middleware stack. This should be done after parsers and session middleware but before routing middleware.

```typescript
app.use(passport.initialize());
app.use(passport.session());
```

## Authentication

### Default Callback

By default the `verify` callback in the Strategy will call the passport default `done` callback function which calls `req.login()` implicitly. This returns a `401` status if login fails for any reason other than an internal error which returns a `500` status.

```typescript
app.post('/login', passport.authenticate('local'), (req, res) => {
    // If this function gets called, authentication was successful.
    // `req.user` contains the authenticated user.
    res.redirect('/users/' + req.user.username);
});
```

You can supply redirects for success and failure which send a `302` status instead of `402`

Failure flashes send the information message in the verify callback to the user. This requires a `req.flash()` function which was removed from express in `3.x` . A third party middleware can add this back in if needed.

```typescript
app.post('/login',
  passport.authenticate('local', { successRedirect: '/',
    failureRedirect: '/login',
    failureFlash: true }),
  (req, res) => {}
);
```

### Custom Callback

Instead of using `passport.authenticate()` as a middleware you can supply a custom `done` callback to handle login logic inside the request handler. This will then be called from inside the `verify` callback instead of the passport default `done` callback.

```typescript
app.post('/login' (req, res, next) => {
  passport.authenticate("local", (err: Error, user: User, info: string) => {
    if (err) return next(err);
  
    if (!user) {
      console.error("No user was found");
      return res.redirect("/login");
    }
  
    req.logIn(user, (err: Error) => {
      if (err) return next(err);
  
      console.info(`Successfully logged in as ${user.username}`);
  
      res.send(`Successfully logged in as ${user.username}`);
    });
  })(req, res, next);
});
```



