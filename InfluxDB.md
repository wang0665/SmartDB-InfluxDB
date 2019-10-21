## InfluxDB Basic

We are using InfluxDB for our database. It is a time series database.

### important note for operating the DB

* DO NOT do a heavy query such as more than 12 hours data query, schedule a task and do a periodic query and summary to reduce the load of the server
* DO NOT share the ip address, user name, password with other's people

### Visualization tools for InfluxDB

- Suppose you IP address is 127.0.0.1 [replace this accordingly]

- The visualization address will be 127.0.0.1:8888.

- The manual of how to use Chronograf is [here](https://docs.influxdata.com/chronograf/v1.7/)

- This tool provides an easy way to understand the DB base structure and you can do some simple plot to better understand the structure.


The Database name is "SDB"

The SERIES name is "SecondlyReading"

For each device there will be a unique ID which in the database is named as "DeviceID"

Each device will include 10 channel which is name as "ChannelId"
