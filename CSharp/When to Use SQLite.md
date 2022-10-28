# When to Use SQLite
Basically, you want to avoid using sqlite when you have a lot of write concurrency or need to scale to terabytes of data. In many other cases, sqlite is a surprisingly good alternative to a "traditional" database such as MySQL.

Sqlite is an embedded database which has no network capabilities.

If you need:
- Network access - For example accessing from another machine.
- Any real degree of concurrency - For example, if you think you are likely to want to run several queries at once, or run a workload that has lots of selects and a few updates, and want them to go smoothly etc.
- A lot of memory usage - For example, to buffer parts of your 1Tb database in your 32G of memory.

Then you need to use mysql or some other server-based RDBMS.


