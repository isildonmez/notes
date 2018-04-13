> From [Odin Project's curriculum](https://www.theodinproject.com/courses/ruby-on-rails/lessons/a-railsy-web-refresher)

Cookies are basically a way for websites to remember who you are from one request to another. Remember – every HTTP request is totally independent of each other one. Meaning that when you go to the Home page of a website and then click on a link to their About page, the web server treats you as a completely new user.

…Unless they’ve given you some cookies (which they almost certainly have). Cookies are little bits of data that your browser sends to the website every time you make a request to it. From the perspective of the web server, it lets the server identify you as the same person who made any of a series of previous requests. It preserves the *state* of your session.

Go to a website you normally frequent, open up your developer tools, and find the cookies. In Chrome, it’s by clicking on “Application” tab then “cookies” on the leftmost menu. You’ll see them as name-value pairs. Often there will be something like a “user_session” or “token” variable that is some unintelligible string of characters.

-----------

> From this [link](http://www.allaboutcookies.org/)

## What are cookies in computers?

Also known as browser cookies or tracking cookies, cookies are small, often encrypted text files, located in browser directories. They are used by web developers to help users navigate their websites efficiently and perform certain functions. Due to their core role of enhancing/enabling usability or site processes, [disabling cookies](http://www.allaboutcookies.org/manage-cookies/) may prevent users from using certain websites.

Cookies are created when a user's [browser](http://www.allaboutcookies.org/faqs/browser.html) loads a particular website. The website sends information to the browser which then creates a text file. Every time the user goes back to the same website, the browser retrieves and sends this file to the website's server. Computer Cookies are created not just by the website the user is browsing but also by other websites that run ads, widgets, or other elements on the page being loaded. These cookies regulate how the ads appear or how the widgets and other elements function on the page.For Managing cookies for different browsers [see here](http://www.allaboutcookies.org/manage-cookies/)