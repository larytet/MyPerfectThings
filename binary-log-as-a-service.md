*Intro*

We developers want to collect as much of debug data as possible, keep the collected logs infinitely. We rarely if ever view the collected data, but we insist on the real-time 24/7 access to the collected logs. This set of requirements creates a challenge for devops teams leading to expensive solutions like logz.io, vastdata, etc . Binary logs can address these requirements by reducing the storage needs, simplifying the processing, enforcing logging discipline in the source code. 

Binary log can reduce I/O load and save CPU in the application. Both generation and  output of the binary log can be significantly cheaper. 

Depending on the architecture binary log can reduce the amount of "events" needed to be processed by the log processing pipeline. Aggregation, filtering, deduplication, grouping - these operations are getting easier. 


The data compression phase, if supported, is not zero cost. For example, the IoT world there is a case for generating and collecting binary logs. 


Based on https://github.com/larytet/binlog/ for example,

* Collect binary logs
* Generate schemas, index on the fly
* Store the log in the ElastiSearch/CouchDB
* Add server side script converting the logs into a human readable format

*Applications*

* IoT world
* Automation
* High performance WEB applications
* Kernel code


Links

* https://www.baryudin.com/blog/entry/binary-self-contained-logs-modern-high-throughput-systems/
