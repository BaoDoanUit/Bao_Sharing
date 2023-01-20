
[Google File System](https://medium.com/geekculture/google-file-system-architecture-cdeabef3f1ea?source=list-aaa0a6895331--------2-------predefined%3Aaaa0a6895331%3AREADING_LIST---------------------)

It is a large distributed system build on cheap servers. It regards server failure as a normal phenomenon and is automatically fault-tolerant through software, which greatly reduces the cost of the system while ensuring its reliability and availability of the system.

#### The characteristics of Google Applications
1. The datatset is huge
2. The data access is mostly sequential access
3. Multi-client concurrent append scenarios
4. Random write behavior is rare
5. Write once, read multiple times