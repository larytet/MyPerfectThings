# Introduction

Developers often collect far more debug data than they actually use, and then retain it indefinitely. In practice, most of these logs are rarely reviewed. This creates a serious burden for DevOps teams, who are then forced to rely on costly storage and processing solutions such as Logz.io or Vast Data.

Binary logging offers a practical alternative. By storing logs in a compact binary format, organizations can significantly reduce storage requirements, simplify downstream processing, and encourage better discipline in what is logged at the source.

Binary logs can also reduce I/O overhead and CPU usage within applications. Both log generation and log output can be significantly cheaper than with text-based logging. Depending on the system architecture, binary logging can also reduce the number of events that need to pass through the processing pipeline. Operations such as filtering, aggregation, deduplication, and grouping become easier and more efficient.

Although compression is not free and still carries some processing cost, binary logs remain especially attractive in environments where efficiency matters most. This is particularly true in IoT systems, where devices often need to generate and transmit logs under strict storage, bandwidth, and power constraints.

# Implementation

One example of a binary logging system is the [binlog](https://github.com/larytet/binlog/) project on GitHub. It demonstrates several useful capabilities:

- Collect logs in binary form
- Use standard serialization formats such as Protobuf, FlatBuffers, or Cap’n Proto
- Generate schemas and index log entries on the fly
- Store logs in backends such as Elasticsearch or CouchDB
- Support server-side conversion of binary logs into human-readable form

# Applications

Binary logs are valuable in a wide range of systems, including:

- IoT devices
- Automation systems
- High-performance web applications
- Kernel-level code

# Links

* https://www.baryudin.com/blog/binary-self-contained-logs-modern-high-throughput-systems/
* https://engineering.fb.com/2019/10/07/data-infrastructure/scribe/
* https://engineering.fb.com/2017/08/31/core-data/logdevice-a-distributed-data-store-for-logs/
* https://www.elastic.co/beats/filebeat
