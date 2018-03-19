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















