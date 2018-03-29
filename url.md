> From [this article by Matt Cutts](http://www.mattcutts.com/blog/seo-glossary-url-definitions/)

Here’s a valid URL which has lots of components:

http://video.google.co.uk/videoplay?docid=-7246927612831078230&hl=en#00h02m30s

Here are some of the components of the url:

- The protocol is http. Other protocols include https, ftp, etc.
- The host or hostname is video.google.co.uk.
- The subdomain is video.
- The domain name is google.co.uk.
- The top-level domain or TLD is uk. The uk domain is also referred to as a country-code top-level domain or ccTLD. For google.com, the TLD would be com.
- The second-level domain (SLD) is co.uk.
- The port is 80, which is the default port for web servers. Other ports are possible; a web server can listen on port 8000, for example. When the port is 80, most people leave out the port.
- The path is /videoplay. Path typically refers to a file or location on the web server, e.g. /directory/file.html
- This URL has parameters. The name of one parameter is docid and the value of that parameter is `-7246927612831078230`. URLs can have lots parameters. Parameters start with a question mark (?) and are separated with an ampersand (&).
- See the “#00h02m30s”? That’s called a fragment or a named anchor. The Googlers I’ve talked to are split right down the middle on which way to refer it. Disputes on what to call it can be settled with arm wrestling, dance-offs, or drinking contests. 🙂 Typically the fragment is used to refer to an internal section within a web document. In this case, the named anchor means “skip to 2 minutes and 30 seconds into the video.” I think right now Google standardizes urls by removing any fragments from the url.

**What is a static url vs. a dynamic url?**

Technically, we consider a static url to be a document that can be returned by a webserver without the webserver doing any computation. A dynamic url is a document that requires the webserver to do some computation before returning the web document.

Some people simplify static vs. dynamic urls to an easier question: “Does the url have a question mark?” If the url has a question mark, it’s usually considered dynamic; no question mark in the url often implies a static url. That’s not a hard and fast rule though. For example, urls that look static like http://news.google.com/ may require some computation by the web server. Most people just refer to urls as static or dynamic based on whether it has a question mark though.