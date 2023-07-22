Summary of how we scale our system to support millions of users:
- [Keep web tier stateless](./stateless_web_tier_byte_byte_go.md)
- Build redundancy at every tier
- [Cache data as much as you can](./cache_byte_byte_go.md)
- Support multiple data centers
- [Host static assets in CDN](./cdn_byte_byte_go.md)
- [Scale your data tier by sharding](./db_scaling_byte_byte_go.md)
- Split tiers into individual services
- [Monitor your system and use automation tools](./logging_metrics_automation_byte_byte_go.md)


See also these related notes:
- [Data Centers](./data_centers_byte_byte_go.md)
- [Databases](./db_byte_byte_go.md)
- [Message Queues](./message_queue_byte_byte_go.md)

See [this useful site](https://bytebytego.com/courses/system-design-interview/scale-from-zero-to-millions-of-users)