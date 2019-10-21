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

The version of the InfluxDB is 1.7

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

**For each Smart DB hardware, there will be 10 channels correspond to 10 physical circuit breakers of the Distribution Box/Board. The information of each individual circuit breaker (In the database we name them as "ChannelID") can be selected and queried. The information of each circuit breaker is listed in the next part.**

### Fields

_The "Fields" include the specific data/information that each circuit breaker be recorded. The detailed information about Fields, please refer to InfluxDB [manual](https://docs.influxdata.com/influxdb/v1.7/)_

- [Frequency]
- [ApparentPower]
- [RMSCurrent]
- [RMSVoltage]
- [ReactivePower]
- [RealPower]

Item Name | Description
------------ | -------------
"Frequency" | The voltage / network frequency of the circuit breaker, under normal circumstances, all circuit breaker frequencies are the same as the frequency of the power grid, because the frequency of the power grid is basically constant.
"ApparentPower" | Apparent Power of the circuit breaker. Didn't use in this project
"RMSCurrent" | RMS Current of the circuit breaker. How much current has been pass through the circuit breaker?
"RMSVoltage" | RMS Voltage of the circuit breaker. What is the voltage of each circuit breaker? (All circuit breakers should have the same value))
"ReactivePower" | Reactive Power of the circuit breaker. Didn't use in this project
"RealPower" | Real Power of the circuit breaker. **This is the important information in this project**

### Query Example


In this particular example, we want to get device ID = 0000, Channel ID = 1, the RMS current average value from 2018-05-31T00:00:00.000Z (UTC time) to 2018-05-31T01:00:00.000Z (UTC time). The average is based on 5 minute time window (means every 5 minutes make an average of that 5 minutes and return one value) 

```
SELECT mean("RMSCurrent") AS "mean_Val" FROM "SDB"."basicRetention"."SecondlyReading" WHERE time > '2018-05-31T00:00:00.000Z' AND time < '2018-05-31T01:00:00.000Z' AND "ChannelId"='1' AND "DeviceId"='0000' GROUP BY time(5m)
```

In this particular example, we want to get device ID = 000012, Channel ID = 1, the Real Power value from 2019-10-21T00:00:00.000Z (UTC time) to 2019-10-21T01:00:00.000Z (UTC time). There is no average process.

```
SELECT "RealPower" AS "Real_P" FROM "SDB"."basicRetention"."SecondlyReading" WHERE time > '2019-10-21T00:00:00.000Z' AND time < '2019-10-21T01:00:00.000Z' AND "ChannelId"='1' AND "DeviceId"='000012'
```

For more detail about how to query, please refer to [InfluxDB Manual](https://docs.influxdata.com/influxdb/v1.7/)

### Programming Interface 

InfluxDB support Python this lib is [here](https://github.com/influxdata/influxdb-python)

InfluxDB support Java this lib is [here](https://github.com/influxdata/influxdb-java)

InfluxDB support PHP this lib is [here](https://github.com/influxdata/influxdb-php), **I didn't use this**
