> From the curriculum of [Odin Project](https://www.theodinproject.com/courses?ref=homenav) and from [this link](https://www.theodinproject.com/courses/ruby-on-rails/lessons/a-railsy-web-refresher)

### HTTP

HTTP is just a way of structuring the request-and-response conversation between your browser and the server. Actually, it’s not even a conversation since it is stateless… it’s more of an “ask and receive”. The protocol outlines how that brief piece of dialogue should occur.

One key component to pay attention to is the fact that the request and response both have header and (usually) body components. The header contains information about the request or response itself (meta data), including which website to send or return to and what the status of the response is. The body of the request can contain things like data submitted by a form or cookies or authentication tokens while the response will usually contain the HTML page you’re trying to access.

The other key component is that each request uses one of four main “verbs” – GET, POST, PUT, and DELETE. These days, you almost only see GET and POST requests (even if you’re trying to do a delete of something they usually fake it using a POST request), but it’s important to understand the difference between the verbs.

Please check [this file](./http.md) for more about HTTP.