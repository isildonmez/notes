### Elasticsearch: Fast, Incisive Search against Large Volumes of Data

Conventional SQL database managements systems aren't really designed for full-text searches, and they certainly don't perform well against loosely structured raw data that resides outside the database. On the same hardware, queries that would take more than 10 seconds using SQL will return results in under 10 milliseconds in Elasticsearch.

### Proxy

![](./images/fw_proxy_vs_reverse_proxy.png)

### Redis vs DB(Postgres)

- Redis is a key-value storage system that operates in RAM memory, it's like a "light database" and since it works at RAM memory level it's orders of magnitude faster compared to reading/writing to PostgreSQL or any other traditional Relational Database.

- Redis is a so-called NoSQL database, like Mongo and many others. It can't directly replace PostgreSQL, you still want permanent storage, but it works along with Relational Databases as an alternate storage system. You can use Redis if your IO operations start getting expensive and it's great for quick calculations and key-based queries.

### Redis Keys

Redis keys are binary safe, this means that you can use any binary sequence as a key, from a string like "foo" to the content of a JPEG file. The empty string is also a valid key.

- Try to stick with a schema. For instance "object-type:id" is a good idea, as in "user:1000". Dots or dashes are often used for multi-word fields, as in "comment:1234:reply.to" or "comment:1234:reply-to".

### Github vs Bitbucket

- **Github** offers unlimited free repositories (with colloboration) for open-source repos while charging for private repos. **Bitbucket** allows unlimited free private repos while charging for more than a certain number of collaborators.

- **Gitlab** offers a hosted version as well, and unlimited public and private repos.
