# Passport-UserApp

Password authentication strategy using [UserApp](https://www.userapp.io) for [Passport](http://passportjs.org/).

*UserApp is a cloud-based user management API for web apps with the purpose to relieve developers from having to program logic for user authentication, sign-up, invoicing, feature/property/permission management, and more.*

This module lets you authenticate using a username and password in your Node.js
applications. By plugging into Passport, UserApp authentication can be easily and
unobtrusively integrated into any application or framework that supports
[Connect](http://www.senchalabs.org/connect/)-style middleware, including
[Express](http://expressjs.com/).

## Installation

    $ npm install passport-userapp

## Usage

#### Configure Strategy

The userapp authentication strategy authenticates users using a username and
password via a REST call to UserApp. The strategy requires a `verify` callback, which accepts these
credentials and calls `done` providing a user. To be able to use this strategy, you need a [UserApp account](https://app.userapp.io/#/sign-up/), with an [App Id](https://help.userapp.io/customer/portal/articles/1322336-how-do-i-find-my-app-id-).

    passport.use(new UserAppStrategy({
            appId: 'YOUR-APP-ID'
        },
        function (userprofile, done) {
            Users.findOrCreate(userprofile, function(err,user) {
                if(err) return done(err);
                return done(null, user);
            });
        }
    ));

#### Authenticate Requests

Use `passport.authenticate()`, specifying the `'userapp'` strategy, to
authenticate requests.

For example, as route middleware in an [Express](http://expressjs.com/)
application:

    app.post('/login', 
      passport.authenticate('userapp', { failureRedirect: '/login' }),
      function(req, res) {
        res.redirect('/');
      });

## Examples

For a complete, working example, refer to the [login example](https://github.com/userapp-io/passport-userapp/tree/master/examples/login).

## License

(The MIT License)

Copyright (c) 2013 UserApp

Permission is hereby granted, free of charge, to any person obtaining a copy of
this software and associated documentation files (the "Software"), to deal in
the Software without restriction, including without limitation the rights to
use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of
the Software, and to permit persons to whom the Software is furnished to do so,
subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS
FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR
COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER
IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN
CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
