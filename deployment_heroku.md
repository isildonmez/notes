> From [Odin Project's curriculum](https://www.theodinproject.com/courses/ruby-on-rails/lessons/deployment)

## Heroku Overview

Heroku is great for beginners because it’s a free and “simple” push-to-deploy system. Their system is actually built on EC2 but it saves you a lot of hassle. Because of this, when you DO get to the paid tiers, it will be more expensive than EC2 but should be worth it for a while. The best part is that you get free high quality hosting for any number of new apps.

### Instances and Traffic

Heroku works by giving you virtual “Dynos” which run your app. Basically, one dyno means one instance of your application running at one time. That’s sort of like having a single computer run your app, like you do on Localhost. Multiple dynos is like having several copies of your app running simultaneously, which allows you to handle more traffic. The cool thing about Rails is that you can always fire up more instances of your application if you start getting too much traffic and users start having to wait for their requests to be filled.

For most of your apps, one dyno is plenty enough. You can support a lot of traffic using just a single dyno, and Heroku gives you your first one for free. Unfortunately, if you don’t visit your app for a while, Heroku will “shut down” the dyno and basically stop running your app continuously. They don’t want to waste resources supporting the thousands of apps that no one visits.

This means that, the first time someone visits your site in a while, it will take 30-40 seconds to “fire up” a dyno with your app on it. There are a couple solutions to this – you can pay for an additional dyno, in which case Heroku will never idle any of your dynos, or you can set up another service to periodically ping your application (e.g. NewRelic, see below).

Heroku lets you do your application management either from the command line (using the “Heroku CLI” set of commands) or by going to their website and clicking around. Pretty much all the functions are available in both places, which is handy.

### Domains and Naming

Heroku will give you a random application name when you first deploy, something zen like “afternoon-falls-4209”. If you want to visit the app, you can either type `$ heroku open` on the command line or just go directly to `http://afternoon-falls-4209.herokuapp.com`.

- *Note: If you change your app’s name on Heroku, you’ll probably need to manually update your Git remote so Git knows where to send your local application when you deploy to Heroku.*

That domain name will always be yours on Heroku. Obviously, in the real world, you want to link it to a custom domain of your own, e.g. `http://my_cool_domain.com`. First you’ll obviously need to purchase the domain from a registrar like GoDaddy or IWantMyName. Try using [Domainr](http://domai.nr/) to find new domains, it’s great.

Once you have your own domain, you will need to go in and point it to your `herokuapp.com` subdomain by changing the appropriate entry in your CNAME file. Where does `mail.yourapp.com` or `www.yourapp.com` or `calendar.yourapp.com` go? That file, which lives at your Registrar, basically defines where incoming requests should go. These settings are relatively easy to change but take several hours to take effect.

You’ll also need to tell Heroku that you’d like to point your app to a custom domain. See the [Heroku Custom Domains Help File](https://devcenter.heroku.com/articles/custom-domains) for detailed instructions.

### Addons

These are third party applications which have been designed to seamlessly add onto your own. You can view the ones you have via the command line using `$ heroku addons` or add a new one using something like `$ heroku addons:add newrelic:standard`. You can also work from the web interface.

[This article on Heroku Help](https://devcenter.heroku.com/articles/managing-add-ons) talks about how to work with addons.

Some of the most useful ones to you will be:

1. [New Relic](https://devcenter.heroku.com/articles/newrelic) – It is an application monitoring and analytics service, so you know when your application has gone down or where your bottlenecks are. They have a free plan which is useful for analytics.
2. [PGBackups](https://devcenter.heroku.com/articles/pgbackups) – this add-on lets you make backups of your database. There’s nothing worse than losing data, and so this app will make your life a lot easier. The free tier lets you manually download backups or set up rake tasks to do the same.
3. [SendGrid](https://devcenter.heroku.com/articles/sendgrid) is an email service, which we’ll cover more later. You can’t send email without help and it’s actually incredibly complex behind the scenes. This add-on makes your life a lot easier by doing most of it for you.
4. Visit [Heroku Addons Center](https://addons.heroku.com/) for more information on available addons.

Note that you’ll probably be prompted for your billing information when installing add-ons (or possibly before) because they need to be able to charge for overages.

## Deploying to Heroku

A typical convention with Heroku commands is that they’re prefixed with either `$ heroku run` or just `$heroku`, so running a database migration on Heroku is `$ heroku run rails db:migrate` and using the console is `$ heroku run console`.

- Create a new Heroku application from the command line using `$ heroku create`. This will also add a new remote to your Git setup so that Git knows where to push your app (so you don’t need to worry about that).
- Push using the command `$ git push heroku master`.
- The last step you’ll need to do is manually set up your database. Any time you run migrations or otherwise alter your database, you will need to remember to also run them on Heroku. If it’s your first database, you’ll likely do something like `$ heroku run rails db:migrate`.

### What's going on?

When you created the new Heroku app, you also automatically set up the “heroku” remote to point to your application on Heroku. When you execute `$ git push heroku master`, Git will just ship your code up to Heroku.

From there, Heroku more or less does what you do for your own localhost. First, it will take the “slug” of code and files that you uploaded, identify your Ruby version, and run a `$ bundle install`. It sets up your database connection and then runs the asset pipeline.

In development, Rails only partially executes the asset pipeline – it runs all the preprocessors but serves asset files like stylesheets and javascripts individually (check your local server logs to see it serving dozens of individual files). In production, Heroku will finish the job by not only running the preprocessors but also mashing your assets into those single files with the timestamp names (check out the source code of this page for an example – as I type the stylesheet is called `assets/application-1fc71ddbb281c144b2ee4af31cf0e308.js`).

So it doesn’t have to run this part of the asset pipeline (which won’t actually change at all from one visit to the next) every single time a new HTTP request is served, Heroku will “precompile” the assets up front and serve them from the cache.

Once precompilation is complete, Heroku will fire up a dyno with your application on it and you should be able to visit it within 30 seconds or so by running $ heroku open or just navigating directly to the application’s address.

### Essential Heroku Commands

- `$ heroku run rails db:migrate`
- `$ heroku run console` gives you a Rails console, though in Production (so don’t mess around with things, this is real data!)
- `$ heroku logs -t` shows you your server logs (like you’re used to when running `$ rails server`) on a streaming basis (which is the result of the -t, or “tail” flag). See [this Heroku post](https://devcenter.heroku.com/articles/logging) for more information on logging.
- `$ heroku restart` – for if your application has failed and won’t start up. See [this SO post](http://stackoverflow.com/questions/14612695/heroku-how-can-i-restart-my-rails-server) for more.

## Learning to Love Heroku: Errors

See [Heroku’s brief guide on diagnosing errors](https://devcenter.heroku.com/articles/error-pages) for a good way to start. It also talks about creating your own error messages for Heroku to use.

## 500’s While Running the Application

Heroku serve up a 500 error regardless of which error your application threw, which makes it doubly frustrating to diagnose them. You’ll want to open up the Heroku logs (`$ heroku logs -t`) to check out the server output.

- If this is your first deployment and your very first page served up a 500, did you remember to migrate your database? That’s a common one.
- Other 500 errors will just have to be tracked down using the logs. It should incentivize you to build useful error messages into [your application logs](https://devcenter.heroku.com/articles/logging)!
- Another common class of errors is related to switching from an SQLite3 database in development to the PostgreSQL one in production (another reason you should wean yourself off SQLite3 and use PG in development as soon as possible). There are just some little things, especially if you’re using direct SQL code or `true`/`false` in your ActiveRecord queries (in PG it’s `t`/`f`). Postgres errors can be annoying to diagnose so it’s usually best to get them over with in development (when you can operate much faster) than to combine them with any errors you may have in deployment.
- Remember Environment Variables (aka “Config vars”)? If you’ve got any gems or add-ons which require special tokens or API codes that you shouldn’t hardcode into your application, you will need to tell Heroku what those variables are. This is another tricky one to diagnose because often times these gems will fail silently and you’ll be left wondering why they didn’t work.

To get your environment variables to Heroku, you can either manage them using a gem like `figaro` (see [docs here](https://github.com/laserlemon/figaro)) or [directly upload them](https://devcenter.heroku.com/articles/config-vars) with a command like `$ heroku config:set YOUR_VARIABLE=some_value`. This will make that variable available to all instances of your application running on Heroku (you won’t need to reset it each time either).

### Localhost Tricks and Tips

Dialing things back to the local environment, here are a few useful things to know to help you work more efficiently in development:

- Use `$ rails server -p 3001` to create a Rails server on a different port (in the example, port 3001). This way you can run multiple Rails apps at the same time. Just go to http://localhost:3001 now to access the new app.

- Check the [documentation](https://devcenter.heroku.com/articles/getting-started-with-rails5) for a step-by-step guide to deploying.

- Check the [documentation](https://devcenter.heroku.com/articles/how-heroku-works) for a better understanding how heroku works



















