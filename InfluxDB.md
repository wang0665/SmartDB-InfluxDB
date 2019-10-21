## InfluxDB Basic

We are using InfluxDB for our database. It is a time-series database.

The manual of InfluxDB can be found at [here](https://docs.influxdata.com/influxdb/v1.7/)

Please read this before you do any coding

### Important note for operating the DB

* DO NOT do a heavy query such as more than 12 hours data query, schedule a task and do a periodic query and summary to reduce the load of the server
* DO NOT share the ip address, user name, password with other's people

### Visualization tools for InfluxDB [Chronograf]

- Suppose you IP address is 127.0.0.1 [replace this accordingly]

- The visualization address will be 127.0.0.1:8888.

- The manual of how to use Chronograf is [here](https://docs.influxdata.com/chronograf/v1.7/)

- This tool provides an easy way to understand the DB base structure and you can do some simple plot to better understand the structure.

## Database Structure

### Measurements & Tags

_The detailed information about Measurements & Tags, please refer to InfluxDB [manual](https://docs.influxdata.com/influxdb/v1.7/)_

- [SDB]
  - [SecondlyReading]
    - [DeviceID]
      - 0111 (examlpe only)
      - 0901 (examlpe only)
      - xxxx
      - ....
    - [ChannelId]   
      - 0
      - 1
      - ...
      - 9
      

Item Name | Description
------------ | -------------
"SDB" | This is the database name which Smart DB data were stored
"SecondlyReading" | This is the series name which Smart DB raw data were stored
"DeviceID" | This is used to trace/select a specified device based on its unique ID
"ChannelId" | This is used to trace/select a specified channnel based on the channel

**For each Smart DB hardware, there will be 10 channel correspond to 10 physical circuit breaker of the Distribution Box/Board. The information of each individual circuit breaker (In the database we name them as "ChannelID") can be selected and queried. The information of each circuir breaker are shown as next part **
