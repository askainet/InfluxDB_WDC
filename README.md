# InfluxDB_WDC
A Tableau Web Data Connector (WDC) to pull data from [InfluxDB](https://github.com/influxdata/influxdb)

## Instructions

### Local install
* npm install influxdb_wdc
  OR
* Download the InfluxDB* files and put them in a web server directory.  (The only dependency is ['bootstrap-show-password.js'](https://raw.githubusercontent.com/wenzhixin/bootstrap-show-password/master/bootstrap-show-password.js) and if you don't install it the only part that won't work is the show/hide password button.)

* Open in Tableau 10.2+ and point to your URL.

### Use it in place

This is hosted by Github Pages.  To use it, open Tableau (10.2+), select "Web Data Connector" and point to this URL: https://tagyoureit.github.io/InfluxDB_WDC/InfluxDB.html?auth=true

#### Authorization
If you use authorization on your InfluxDB, you can click the link to reload the page with the username/password fields. Alternatively, add `?auth=true` or `?auth=false` to the end of the URL to access these directly.


## Suggestions on use
### Tableau and Time Series
Tableau works great with time data, but time series metrics can be a challenge.  The most metrics you can have on a single graph is 2 (with Dual Axis).  If you want to show many metrics you'll want to create a dashboard with individual measurements.

### Aggregation
Aggregation is a great way to be able to do a row-level join on time series data that would otherwise not be joinable.  When you aggregate to any interval, Influx will "fill in" the missing values with nulls.  This should enable an inner join where you can use all of your data from a single Tableau Data Source.  In Tableau, use your table with earliest/latest dates and then connect to it with a left-outer join.

Aggregation can significantly decrease (or increase) the number of data points that are returned.  If your DB stores 1000 measurements per second, and aggregate up to the minute you'll reduce the data by 59,999 points per minute.  On the other hand, if you store 1 measurement per hour and aggregate by the milli-second you'll pull an extra 59,999 data points per minute.

If you don't aggregate the measurements, then you will likely want to create a separate Tableau Data Source for each measurement.  

## Limitations

Currently, the admin user is needed to populate the list of databases.  Once the extract is created if you want to refresh it you can enter a read (or write) only user account in Tableau.