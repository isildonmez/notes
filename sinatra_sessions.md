From Sinatra [README](http://sinatrarb.com/intro.html#Using%20Sessions)

## Using Sessions

A session is used to keep state during requests. If activated, you have one session hash per user session:

```
enable :sessions

get '/' do
  "value = " << session[:value].inspect
end

get '/:value' do
  session['value'] = params['value']
end
```

### Session Secret Security

To improve security, the session data in the cookie is signed with a session secret using `HMAC-SHA1`. This session secret should optimally be a cryptographically secure random value of an appropriate length which for `HMAC-SHA1` is greater than or equal to 64 bytes (512 bits, 128 hex characters). You would be advised not to use a secret that is less than 32 bytes of randomness (256 bits, 64 hex characters).

By default, a 32 byte secure random session secret is generated for you by Sinatra, but it will change with every restart of your application. If you have multiple instances of your application, and you let Sinatra generate the key, each instance would then have a different session key which is probably not what you want.

For better security and usability it’s recommended that you generate a secure random secret and store it in an environment variable on each host running your application so that all of your application instances will share the same secret. You should periodically rotate this session secret to a new value. Here are some examples of how you might create a 64 byte secret and set it:

#### Session Secret Generation

```
$ ruby -e "require 'securerandom'; puts SecureRandom.hex(64)"
99ae8af...snip...ec0f262ac
```

#### Session Secret Generation (Bonus Points)

Use the [sysrandom gem](https://github.com/cryptosphere/sysrandom) to prefer use of system RNG facilities to generate random values instead of userspace `OpenSSL` which MRI Ruby currently defaults to:

```
$ gem install sysrandom
Building native extensions.  This could take a while...
Successfully installed sysrandom-1.x
1 gem installed

$ ruby -e "require 'sysrandom/securerandom'; puts SecureRandom.hex(64)"
99ae8af...snip...ec0f262ac
```

#### Session Secret Environment Variable

Set a `SESSION_SECRET` environment variable for Sinatra to the value you generated. Make this value persistent across reboots of your host. Since the method for doing this will vary across systems this is for illustrative purposes only:

```
# echo "export SESSION_SECRET=99ae8af...snip...ec0f262ac" >> ~/.bashrc
```

#### Session Secret App Config

Setup your app config to fail-safe to a secure random secret if the `SESSION_SECRET` environment variable is not available.

```
require 'securerandom'
# -or- require 'sysrandom/securerandom'
set :session_secret, ENV.fetch('SESSION_SECRET') { SecureRandom.hex(64) }
```

### Session Config

If you want to configure it further, you may also store a hash with options in the `sessions` setting:

```
set :sessions, :domain => 'foo.com'
```

To share your session across other apps on subdomains of foo.com, prefix the domain with a `.` like this instead:

```
set :sessions, :domain => '.foo.com'
```

### Choosing Your Own Session Middleware

Note that `enable :sessions` actually stores all data in a cookie. This might not always be what you want (storing lots of data will increase your traffic, for instance). You can use any Rack session middleware in order to do so, one of the following methods can be used:

```
enable :sessions
set :session_store, Rack::Session::Pool
```

Or to set up sessions with a hash of options:

```
set :sessions, :expire_after => 2592000
set :session_store, Rack::Session::Pool
```

Another option is to **not** call enable `:sessions`, but instead pull in your middleware of choice as you would any other middleware.

It is important to note that when using this method, session based protection **will not be enabled by default**.

The Rack middleware to do that will also need to be added:

```
use Rack::Session::Pool, :expire_after => 2592000
use Rack::Protection::RemoteToken
use Rack::Protection::SessionHijacking
```

----------

From [learn.co](https://learn.co/lessons/sinatra-mechanics-of-sessions-readme)

## Sinatra Mechanics Of Sessions Readme

### Setting Up A Session

A session is basically just a hash that stores data on the server and passes that data to the client as a cookie.

In Sinatra, we enable sessions within the controller (e.g., `app.rb`) by adding two lines in the `configure` block:

```
configure do
  enable :sessions
  set :session_secret, "secret"
end
```
The `configure` block above is a part of built-in settings that control whether features are enabled or not. In this case, we're enabling the sessions feature.

The next line, set `:session_secret, "secret"`, is an encryption key that will be used to create a `session_id`. A `session_id` is a string of letters and numbers that is unique to a given user's session and is stored in the browser cookie. You can actually set your `session_secret` to anything that you want. Don't worry too much about understanding how the `session_id` works. It's just part of the mechanics behind getting a secure private session working. You probably won't ever need to interact with it.

### Using Sessions

In order to keep track of a current user throughout a session, we need to set up the `session` hash to store the `user_id` in the hash during a controller action.

```
get '/hey' do
  @session = session
end
```

Because we enabled sessions in our app, every controller action has access to the `session` hash.

We stored the `session` hash in the instance variable `@session` so that our views will have access to the session data. In this case, `@session` now looks like this:

```
@session = {
  "session_id"=>
    "dd32f512ee239ad74aa6f10c8cad37ce28d6c6922eff252ed641b1017130fe22",
  "csrf"=> "040e9777d4dfae03bb1e6498f2a75482",
  "tracking"=>{
    "HTTP_USER_AGENT"=> "e193e9e937caa9a19ca483f046281aae77d2216b",
    "HTTP_ACCEPT_LANGUAGE"=> "66eae971492938c2dcc2fb1ddc8d7ec3196037da"
  }
}

```

You can also modify and add data to the `session` hash by adding a key-value pair:

```
get '/hey' do
  session["name"] = "Victoria"
  @session = session
end
```

### Viewing Sessions

#### Viewing in Developer Tools

Even though sessions are created on the server, you can view the contents of the `session` hash as a cookie in your browser using Developer Tools.

We'll be using `Learn.co` in this example.
After logged in, go ahead and open up your browser's Developer Tools. In Chrome, you can do this by right-clicking and selecting `Inspect`. Once the Developer Tools are open, click on the `Application` tab. On the left side of the tools, open up the `Cookies` dropdown, click the `learn.co` cookie, and it will bring up all of the cookies loaded on the site.

#### Viewing in Chrome Settings

You can also see the details of these cookies in the Chrome browser by selecting the hamburger icon in the top right corner and navigating to `Settings`, then at the bottom `Show advanced settings...`, `Privacy` and `Content settings`. You'll see `All cookies and site data...` button. This will bring up a list of all of the sites that your browser has stored cookies from.

### Clearing Sessions

There are several ways to clear a session cookie. The first is to simply log out of the site. That ends the current session, at which point all session cookies are automatically cleared.

You can also clear session cookies from the Developer Tools interface. Simply right-click on a session and select either `Delete` or `Clear All from "learn.co"`.

If you remove the session cookies and refresh the page, you'll notice that you've been logged out of the site.

If you log in to a site from an Incognito window, Chrome will create the cookies needed to run that session, but it will not create any long-term, cached cookies. Because of this functionality, Incognito mode is often helpful while debugging session and cookie issues.
