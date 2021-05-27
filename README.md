# NOTE

There's much better alternatives nowadays. Do not use this setup.

* https://github.com/dsmrreader/dsmr-reader
* https://github.com/psy0rz/p1_dsmr_to_influxdb

<strike>
# smartmeter_influx
Grafana, InfluxDB and a python script to graph your P1 Smart Meter engergy consumption reports.

# InfluxDB

```sql
CREATE USER p1smartmeter WITH PASSWORD 'somethingSafe'

CREATE DATABASE p1smartmeter

GRANT ALL ON p1smartmeter TO p1smartmeter

CREATE RETENTION POLICY raw ON p1smartmeter DURATION 30d REPLICATION 1

ALTER RETENTION POLICY raw ON p1smartmeter DEFAULT

DROP RETENTION POLICY autogen ON p1smartmeter

CREATE CONTINUOUS QUERY cq_smartmeter_daily ON p1smartmeter
    RESAMPLE EVERY 15m BEGIN
        SELECT min("+T") AS "+T_min", max("+T") AS "+T_max",
        spread("+T") AS "+T_spread", min("+T1") AS "+T1_min",
        max("+T1") AS "+T1_max", spread("+T1") AS "+T1_spread",
        min("+T2") AS "+T2_min", max("+T2") AS "+T2_max",
        spread("+T2") AS "+T2_spread", min(G) AS G_min, 
        max(G) AS G_max, spread(G) AS G_spread
            INTO p1smartmeter.raw.smartmeter_daily
            FROM p1smartmeter.raw.smartmeter GROUP BY time(1d) END
```
</strike>
