> From [Odin Project's curriculum](https://www.theodinproject.com/courses/ruby-on-rails/lessons/a-railsy-web-refresher)

## MVC

MVC is all about organization and Rails is all about MVC. Inside your `app` directory, they are highly organized and specifically meant to separate the Model, View, and Controller.

The point of MVC is that the functions of a web application can be broken down into more or less distinct parts. Each part gets its own Ruby class. That’s great for you the developer because, when you want to tweak a specific part of the code base or fix a bug, you know exactly which file to modify and where it is.

## The Path Through MVC

Once a request from a browser comes into your application, at the most basic level:

1. The router figures out which controller to send it to (e.g. for your blog, the Posts controller).
2. That controller asks the model (e.g. Post model) for data and any other tough questions it has.
3. Then that controller passes off whatever data it needs to the views (e.g. `index.html.erb`), which are basically just HTML templates that are waiting for those variables.
4. Once the proper view has been pumped full of the data it needs (like the current user’s name), it gets sent back to the client that made the original request. Presto!

To characterize the three (badly), the model is the supersmart geek in the back room, the controller is the social middleman that talks to everyone but doesn’t really do anything too intensive (it asks the model in those cases), and the view just looks pretty and waits to get its outfit from the controller.

-----------

> From [an article in betterexplained](https://betterexplained.com/articles/intermediate-rails-understanding-models-views-and-controllers/)

## Intermediate Rails: Understanding Models, Views and Controllers

Here’s the big picture as I understand it:

![mvc](images/mvc-rails.png)

- The browser makes a request, such as http://mysite.com/video/show/15

- The web server (mongrel, WEBrick, etc.) receives the request. It uses routes to find out which controller to use: the default route pattern is “/controller/action/id” as defined in `config/routes.rb`.  The web server then uses the dispatcher to create a new controller, call the action and pass the parameters.

- Controllers do the work of parsing user requests, data submissions, cookies, sessions and the “browser stuff”. The best controller is Dilbert-esque: It gives orders without knowing (or caring) how it gets done.

- Models are Ruby classes. They talk to the database, store and validate data, perform the business logic and otherwise do the heavy lifting.

- Views are what the user sees: HTML, CSS, XML, Javascript, JSON. In our example, the controller gives video 15 to the “show” view. The show view generates the HTML: divs, tables, text, descriptions, footers, etc.

- The controller returns the response body (HTML, XML, etc.) & metadata (caching headers, redirects) to the server. The server combines the raw data into a proper HTTP response and sends it to the user.

Many MVC discussions ignore the role of the web server. However, it’s important to mention how the controller magically gets created and passed user information. The web server is the invisible gateway, shuttling data back and forth: users never interact with the controller directly.

### SuperModels

Here’s a few model tips:

#### Using ActiveRecord

```
class User < ActiveRecord::Base
end
```

Ruby can also handle “undefined” methods with ease. ActiveRecord allows methods like “find_by_login”, which don’t actually exist. When you call “find_by_login”, Rails handles the “undefined method” call and searches for the “login” field. Assuming the field is in your database, the model will do a query based on the “login” field. There’s no configuration glue required.


#### Using Attributes

- ActiveRecord grabs the database fields and throws them in an `attributes` array. It makes default getters and setters, but you need to call `user.save` to save them.
- If you want to **override** the default getter and setter, use this:

```
# ActiveRecord: override how we access field
def length=(minutes)
  self[:length] = minutes * 60
end

def length
  self[:length] / 60
end
```

ActiveRecord defines a “`[]`” method to access the raw attributes (wraps the write_attribute and read_attribute). This is how you change the raw data. You can’t redefine length using

```
def length          # this is bad
  length / 60
end
```
because it’s an infinite loop (and that’s no fun). So `self[]` it is.

#### Making new Models

There’s two ways to create new objects:

```
joe = User.new( :name => "Sad Joe" )        # not saved
bob = User.create ( :name => "Happy Bob" )  # saved
```

- `new` does not save to the database: you must call `user.save` explicitly. Method `save` can fail if the model is not valid.
- `User.create` makes a new model and saves it to the database. Validation can fail; `user.errors` is a hash of the fields with errors and the detailed message.

With Ruby’s brace magic, `{}` is not explicitly needed so

```
user = User.new( :name => "kalid", :site => "instacalc.com" )
```

becomes

```
User.new( {:name => "kalid", :site => "instacalc.com"} )
```

#### Using Associations

Suppose users have a “status”: active, inactive, pensive, etc. What’s the right association?

```
class User < ActiveRecord::Base
  belongs_to :status  # this?
  has_one :status     # or this?
end
```

Hrm. Most likely, you want `belongs_to :status`. Yeah, it sounds weird. Don’t think about the phrase “has_one” and “belongs_to”, consider the meaning:

- belongs_to: **links_to** another table. Each user references (links to) a status.
- has_one: **linked_from** another table. A status is linked_from a user. In fact, statuses don’t even know about users – there’s no mention of a “user” in the statuses table at all. Inside class Status we’d write  has_many :users (has_one and has_many are the same thing – has_one only returns 1 object that links_to this one).

These associations actually define methods used to lookup items of the other class. For example, “user belongs_to status” means that `user.status` queries the Status for the proper status_id. Also, “status has_many :users” means that `status.users` queries the user table for everyone with the current `status_id`.

#### Using Custom Associations

Suppose I need two statuses, primary and secondary? Use this:

```
belongs_to :primary_status, :model => 'Status', :foreign_key => 'primary_status_id'
belongs_to :secondary_status, :model => 'Status', :foreign_key => 'secondary_status_id'
```

You define a new field, and explicitly reference the model and foreign key to use for lookups. For example, user.primary_status returns a Status object with the id of “primary_status_id”.

### Quick Controllers

This section is short, because controllers shouldn’t do much besides boss the model and view around. They typically:

- Handle things like sessions, logins/authorization, filters, redirection, and errors.
- Have default methods (added by ActionController). Visiting `http://localhost:3000/user/show` will attempt to call the “show” action if there is one, or automatically render show.rhtml if the action is not defined.
- Pass instance variables like @user get passed to the view.
- Are hard to debug. Use `render :text => "Error found"` and return to do printf-style debugging in your page. This is another good reason to put code in models, which are easy to debug from the console.
- Use sessions to store data between requests: session[:variable] = “data”.

### Using Views

Views are straightforward. The basics:

- Controller actions use views with the same name (method `show` loads  `show.rhtml` by default)
- Controller instance variables (@foo) are available in all views and partials (wow!)

Run code in a view using ERB:

- `<% ... %>`: Run the code, but don’t print anything. Used for if/then/else/end and array.each loops.
- `<%- ...  %>`: Run the code, and don’t print the trailing newline. Use this when generating XML or JSON when breaking up .rhtml code blocks for your readability, but don’t want newlines in the output.
- `<%= ... %>`: Run the code and print the return value, for example: `<%= @foo %>`
- `<%= h ... %>`









