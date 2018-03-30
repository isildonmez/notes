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

> From [an article in betterexplained](https://betterexplained.com/articles/intermediate-rails-understanding-models-views-and-controllers/)

Here’s the big picture as I understand it:

![mvc](images/mvc-rails.png)

- The browser makes a request, such as http://mysite.com/video/show/15

- The web server (mongrel, WEBrick, etc.) receives the request. It uses routes to find out which controller to use: the default route pattern is “/controller/action/id” as defined in `config/routes.rb`.  The web server then uses the dispatcher to create a new controller, call the action and pass the parameters.

- Controllers do the work of parsing user requests, data submissions, cookies, sessions and the “browser stuff”. The best controller is Dilbert-esque: It gives orders without knowing (or caring) how it gets done.

- Models are Ruby classes. They talk to the database, store and validate data, perform the business logic and otherwise do the heavy lifting.

- Views are what the user sees: HTML, CSS, XML, Javascript, JSON. In our example, the controller gives video 15 to the “show” view. The show view generates the HTML: divs, tables, text, descriptions, footers, etc.

- The controller returns the response body (HTML, XML, etc.) & metadata (caching headers, redirects) to the server. The server combines the raw data into a proper HTTP response and sends it to the user.

Many MVC discussions ignore the role of the web server. However, it’s important to mention how the controller magically gets created and passed user information. The web server is the invisible gateway, shuttling data back and forth: users never interact with the controller directly.