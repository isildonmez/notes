> From [Odin Project's curriculum](https://www.theodinproject.com/courses/ruby-on-rails/lessons/a-railsy-web-refresher)

On the server side, you’ll interact with cookies and session variables quite a bit. As mentioned above, one of the main uses of these is to determine who the user is, or “authentication”. You’ll basically retrieve the cookie that the user sends you, use it to find that user in your database, and (if the user exists) then you can display the customized web page for that user.

It’s pretty straightforward in theory, but some of the security implications get a bit hairy so luckily the nice folks at [Platformatec](http://plataformatec.com.br/) created a very handy gem called [“Devise”](https://github.com/plataformatec/devise) which takes care of all this stuff.