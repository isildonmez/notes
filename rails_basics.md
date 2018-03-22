# From toy_project from [Michael Hartl's book](https://www.railstutorial.org/book/toy_app)

------------

#### `rails db:migrate` vs 'rake db:migrate':

It is important to note that in every version of Rails before Rails 5, the `db:migrate` command used `rake` in place of rails, so for the sake of legacy applications it’s important to know how to use Rake.


> **Rake**

> In the Unix tradition, the [Make](https://en.wikipedia.org/wiki/Make_(software)) utility has played an important role in building executable programs from source code. *Rake* is *Ruby make*, a Make-like language written in Ruby.

> Before Rails 5, Ruby on Rails used Rake extensively, so for the sake of legacy Rails applications it’s important to know how to use it. Probably the two most common Rake commands in a Rails context are `rake db:migrate` (to update the database with a data model) and `rake test` (to run the automated test suite). In these and other uses of `rake`, it’s important to ensure that the command uses the version of Rake corresponding to the Rails application’s `Gemfile`, which is accomplished using the Bundler command `bundle exec`. Thus, the migration command

> ```
$ rake db:migrate
```
would be written as

> ```
$ bundle exec rake db:migrate
```

- Rails uses JavaScript to issue the request needed to destroy a user.(If it doesn’t work, be sure that JavaScript is enabled in your browser)