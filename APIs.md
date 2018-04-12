> From [Odin Project's curriculum](https://www.theodinproject.com/courses/ruby-on-rails/lessons/a-railsy-web-refresher)

When your computer or a server (which you’re programming) wants to make a request to another website, it doesn’t bother clicking on things in the browser, it asks that other website for data directly by using that website’s API. An API is just an interface. Our web browser goes in the front door to display a bunch of info from Facebook, and our web server goes in the side door for the same data (much faster and more direct) via the API.

So you want to get data from Google Maps to display on your webpage? You hit its API using the rules specified in its API documentation. Just about every big website makes some portion of its data available via an API and you can too quite easily using Rails.

Not all APIs are web-based. Plenty of them use the same HTTP format but are really just designed to pass data between services. In fact, that’s how the components of Rails are all strung together – they use HTTP to communicate with each other.

There's nothing magical about building your own API – you just tell your controller that you want to respond to requests made by other servers instead of (or in addition to) normal web requests and then specify what exactly you’d like returned (since it probably won’t be an HTML view).

> From this [link](https://money.howstuffworks.com/business-communications/how-to-leverage-an-api-for-conferencing1.htm)

An application-programming interface (API) is a set of programming instructions and standards for accessing a Web-based software application or Web tool. A software company releases its API to the public so that other software developers can design products that are powered by its service.

For example, Amazon.com released its API so that Web site developers could more easily access Amazon's product information. Using the Amazon API, a third party Web site can post direct links to Amazon products with updated prices and an option to "buy now."

An API is a software-to-software interface, not a user interface. With APIs, applications talk to each other without any user knowledge or intervention. When you buy movie tickets online and enter your credit card information, the movie ticket Web site uses an API to send your credit card information to a remote application that verifies whether your information is correct. Once payment is confirmed, the remote application sends a response back to the movie ticket Web site saying it's OK to issue the tickets.

As a user, you only see one interface -- the movie ticket Web site -- but behind the scenes, many applications are working together using APIs. This type of integration is called **seamless**, since the user never notices when software functions are handed from one application to another [source: [TConsult, Inc.](http://www.enginesforwebsites.com/faq/api_application_programming_interface.aspx)]

An API resembles Software as a Service (SaaS), since software developers don't have to start from scratch every time they write a program. Instead of building one core application that tries to do everything -- e-mail, billing, tracking, etcetera -- the same application can contract out certain responsibilities to remote software that does it better.­

Let's use an example of Web conferencing. Web conferencing is SaaS since it can be accessed on-demand using nothing but a Web site. With a conferencing API, that same on-demand service can be integrated into another Web-based software application, like an instant messaging program or a Web calendar.

The user can schedule a Web conference in his Web calendar program and then click a link within the same program to launch the conference. The calendar program doesn't host or run the conference itself. It uses a conferencing API to communicate behind the scenes with the remote Web conferencing service and seamlessly delivers that functionality to the user.