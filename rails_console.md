> From [Rails Console video at Upcase](https://thoughtbot.com/upcase/videos/rails-console)

### Entering the Console

- keep in mind e.g. `rails console test`, default is development
- `rails console --sandbox`: the entire console session will be wrapped in an ActiveRecord transaction, which is rolled back when you exit the console. If you want to create a bunch of test data in the console but not mess up your e.g. development data

### Navigating the Console

- `CTRL-R`
- Mostly the same as [readline cheat sheet](http://readline.kablamo.org/emacs.html)

### Reloading Code

- `reload!`

### Pry

To use Pry when you run `rails console`, add `pry-rails` to your app’s `Gemfile`.

Consider `outcome = Outcome.first`:

- `show-source`: e.g. `show-source outcome.to_s` will show the def of the method
- e.g. `show-source outcome.to_s -s` to see superclass def
- `ls outcome` shows all instance methods of `Outcome`
- `cd outcome` will put me in the scope of that particular instance of `Outcome`. This allows me to directly inspect state, call private methods, etc.

### Special Methods

- `app` method provides access to many high level methods in rails applications such as path helpers (`app.root_path`) and HTTP methods (`app.get(app.root_path)`)
- The `helper` method provides access to view helpers — both those defined by your application and those provided by rails, such as `link_to` 
