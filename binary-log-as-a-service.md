# Introduction

As developers, we often want to collect more debug data than we need and keep it indefinitely, while rarely ever viewing the collected logs. This creates a challenge for devops teams, leading to expensive solutions such as logz.io and vastdata. However, binary logs can address these requirements by reducing storage needs, simplifying processing, and enforcing logging discipline in the source code.

Binary logs can also reduce I/O load and save CPU in the application, as both the generation and output of the binary log can be significantly cheaper. Depending on the architecture, binary logs can reduce the number of "events" needed to be processed by the log processing pipeline. Aggregation, filtering, deduplication, grouping - these operations become easier.

Although the data compression phase, if supported, is not zero cost, binary logs have advantages, especially in the IoT world, where there is a need for generating and collecting binary logs.

Based on https://github.com/larytet/binlog/ for example,

# Implementation

An example of a binary log implementation is the binlog project on GitHub. It provides the following features:

* Collect binary logs
* Use standard serialization like Protobuf, FlatBuffers, Cap’n Proto, etc.
* Generate schemas and index the log entries on the fly
* Store the log in ElastiSearch, CouchDB, etc.
* Add a server-side script converting the logs into a human-readable format.


# Applications

Binary logs are useful in many applications, such as:

* IoT devices
* Automation systems
* High-performance web applications
* Kernel code.

# Links

* https://www.baryudin.com/blog/entry/binary-self-contained-logs-modern-high-throughput-systems/
* https://engineering.fb.com/2019/10/07/data-infrastructure/scribe/
* https://engineering.fb.com/2017/08/31/core-data/logdevice-a-distributed-data-store-for-logs/
* https://www.elastic.co/beats/filebeat
