> From [Odin Project's curriculum](https://www.theodinproject.com/courses/ruby-on-rails/lessons/a-railsy-web-refresher)

Cookies are basically a way for websites to remember who you are from one request to another. Remember – every HTTP request is totally independent of each other one. Meaning that when you go to the Home page of a website and then click on a link to their About page, the web server treats you as a completely new user.

…Unless they’ve given you some cookies (which they almost certainly have). Cookies are little bits of data that your browser sends to the website every time you make a request to it. From the perspective of the web server, it lets the server identify you as the same person who made any of a series of previous requests. It preserves the *state* of your session.

Go to a website you normally frequent, open up your developer tools, and find the cookies. In Chrome, it’s by clicking on “Application” tab then “cookies” on the leftmost menu. You’ll see them as name-value pairs. Often there will be something like a “user_session” or “token” variable that is some unintelligible string of characters.

-----------

> From this [link](http://www.allaboutcookies.org/)

## What are cookies in computers?

Also known as browser cookies or tracking cookies, cookies are small, often encrypted text files, located in browser directories. They are used by web developers to help users navigate their websites efficiently and perform certain functions. Due to their core role of enhancing/enabling usability or site processes, [disabling cookies](http://www.allaboutcookies.org/manage-cookies/) may prevent users from using certain websites.

Cookies are created when a user's [browser](http://www.allaboutcookies.org/faqs/browser.html) loads a particular website. The website sends information to the browser which then creates a text file. Every time the user goes back to the same website, the browser retrieves and sends this file to the website's server. Computer Cookies are created not just by the website the user is browsing but also by other websites that run ads, widgets, or other elements on the page being loaded. These cookies regulate how the ads appear or how the widgets and other elements function on the page.For Managing cookies for different browsers [see here](http://www.allaboutcookies.org/manage-cookies/)

## Standard uses for browser cookies

Website servers set cookies to help authenticate the user if the user logs in to a secure area of the website. Login information is stored in a cookie so the user can enter and leave the website without having to re-enter the same authentication information over and over. [More information](http://www.allaboutcookies.org/cookies/cookies-the-same.html)

[Session Cookies](http://www.allaboutcookies.org/cookies/session-cookies-used-for.html) are also used by the server to store information about user page activities so users can easily pick up where they left off on the server's pages. By default, web pages really don't have any 'memory'. Cookies tell the server what pages to show the user so the user doesn't have to remember or start navigating the site all over again. Cookies act as a sort of “bookmark” within the site. Similarly, cookies can store ordering information needed to make shopping carts work instead of forcing the user to remember all the items the user put in the shopping cart.

[Persistent or tracking Cookies](http://www.allaboutcookies.org/cookies/persistent-cookies-used-for.html) are also employed to store user preferences. Many websites allow the user to customize how information is presented through site layouts or themes. These changes make the site easier to navigate and/or lets user leave a part of the user's “personality” at the site. For Information on session and persistent and tracking cookies, [see here](http://www.allaboutcookies.org/cookies/persistent-cookies-used-for.html).

## Cookie Security and Privacy Issues

Cookies use a plain text format. They are not compiled pieces of code so they cannot be executed nor are they self-executing. Accordingly, they cannot make copies of themselves and spread to other networks to execute and replicate again.

Cookies CAN be used for malicious purposes though. Since they store information about a user's browsing preferences and history, both on a specific site and browsing among several sites, cookies can be used to act as a form of spyware. Many [anti-spyware](http://www.allaboutcookies.org/security/index.html) products are well aware of this problem and routinely flag cookies as candidates for deletion after standard virus and/or spyware scans.See here for some [privacy issues and concerns](http://www.allaboutcookies.org/privacy-concerns/index.html).

The way responsible and ethical web developers deal with privacy issues caused by cookie tracking is by including clear descriptions of how cookies are deployed on their site. If you are a web developer and need advice on implementation of cookies and a privacy policy, you can contact us by the enquiry form at the bottom of the page. These privacy policies should explain what kind of information is collected and how the information is used. Organizations utilising and displaying a proper and useful cookie's policy and privacy policy include: [LinkedIn Networkadvertising.org](https://www.linkedin.com/) and [Dealspotr](https://dealspotr.com/).

Most browsers have built in privacy settings that provide differing levels of cookie acceptance, expiration time, and disposal after a user has visited a particular site. Backing up your computer can give you the peace of mind that your files are safe.

--------

> From [wikipedia](https://en.wikipedia.org/wiki/HTTP_cookie)

Cookies were designed to be a reliable mechanism for websites to remember stateful information (such as items added in the shopping cart in an online store) or to record the user's browsing activity (including clicking particular buttons, logging in, or recording which pages were visited in the past). They can also be used to remember arbitrary pieces of information that the user previously entered into form fields such as names, addresses, passwords, and credit card numbers.

Other kinds of cookies perform essential functions in the modern web. Perhaps most importantly, authentication cookies are the most common method used by web servers to know whether the user is logged in or not, and which account they are logged in with. Without such a mechanism, the site would not know whether to send a page containing sensitive information, or require the user to authenticate themselves by logging in. The security of an authentication cookie generally depends on the security of the issuing website and the user's web browser, and on whether the cookie data is encrypted. Security vulnerabilities may allow a cookie's data to be read by a hacker, used to gain access to user data, or used to gain access (with the user's credentials) to the website to which the cookie belongs (see [cross-site scripting](https://en.wikipedia.org/wiki/Cross-site_scripting) and [cross-site request forgery](https://en.wikipedia.org/wiki/Cross-site_request_forgery) for examples).

The tracking cookies, and especially [third-party tracking cookies](https://en.wikipedia.org/wiki/HTTP_cookie#Third-party_cookie), are commonly used as ways to compile long-term records of individuals' browsing histories – a potential [privacy concern](https://en.wikipedia.org/wiki/Internet_privacy#HTTP_cookies) that prompted European[2] and U.S. lawmakers to take action in 2011.[3][4] European law requires that all websites targeting [European Union](https://en.wikipedia.org/wiki/European_Union) member states gain "informed consent" from users before storing non-essential cookies on their device.

Google Project Zero researcher Jann Horn describes ways cookies can be read by intermediaries, like Wi-Fi hostspot providers. He recommends to use the browser in incognito mode in such circumstances.
