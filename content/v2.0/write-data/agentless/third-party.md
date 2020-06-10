---
title: Third-party technologies
seotitle: Write data with third-party technologies
list_title: Write data with third-party technologies
weight: 103
description: >
Write data to InfluxDB using third-party technologies.
aliases:
menu:
  v2_0:
    name : Third-party technologies
    parent: Agent-less options
---


A number of third-party technologies can be configured to send line protocol directly to InfluxDB.

If you're using any of the following technologies, check out the handy links below to configure these technologies to write data to InfluxDB (**no additional software to download or install**):

- (Write metrics only) [Vector 0.9 or later](#configure-vector)

- [Apache NiFi 1.8 or later](#configure-apache-nifi)

- [OpenHAB 3.0 or later](#configure-openhab)

- [Apache JMeter 5.2 or later](#configure-apache-jmeter)

- [FluentD 1.x or later](#configure-fluentd)

#### Configure Vector

1. On the Vector.dev docs site, see the [InfluxDB Metrics Sink](https://vector.dev/docs/reference/sinks/influxdb_metrics/) page.
2. Under **Configuration**, click **v2** to view configuration settings.
3. Scroll down to [How It Works](https://vector.dev/docs/reference/sinks/influxdb_metrics/#how-it-works) for more detail.

#### Configure Apache NiFi

See the _[InfluxDB Processors for Apache NiFi Readme](https://github.com/influxdata/nifi-influxdb-bundle#influxdb-processors-for-apache-nifi)_ for details.

#### Configure OpenHAB

See the _[InfluxDB Persistence Readme](https://github.com/openhab/openhab-addons/tree/master/bundles/org.openhab.persistence.influxdb)_ for details.

#### Configure Apache JMeter

<!-- after doc updates are made, we can simplify to: See the _[Apache JMeter User's Manual - JMeter configuration](https://jmeter.apache.org/usermanual/realtime-results.html#jmeter-configuration)_ for details. -->

To configure Apache JMeter, complete the following steps in InfluxDB and JMeter.

##### In InfluxDB

1. [Find the name of your organization](https://v2.docs.influxdata.com/v2.0/organizations/view-orgs/) (needed to create a bucket and token).
2. [Create a bucket using the influx CLI](https://v2.docs.influxdata.com/v2.0/organizations/buckets/create-bucket/#create-a-bucket-using-the-influx-cli) and name it `jmeter`.
3. [Create a token](https://v2.docs.influxdata.com/v2.0/security/tokens/create-token/).

##### In JMeter

1. Create a [Backend Listener](https://jmeter.apache.org/usermanual/component_reference.html#Backend_Listener) using the _InfluxDBBackendListenerClient_ implementation.
2. In the **Backend Listener implementation** field, enter _org.apache.jmeter.visualizers.backend.influxdb.influxdbBackendListenerClient_
3. Under **Parameters**, specify the following:
   - **influxdbMetricsSender**: _org.apache.jmeter.visualizers.backend.influxdb.HttpMetricsSender_
   - **influxdbUrl**: _http://localhost:9999/api/v2/write?org=my-org&bucket=jmeter_ (include the bucket and org you created in InfluxDB)
   - **application**: _InfluxDB2_
   - **influxdbToken**: _my-token_ (include the token you created in InfluxDB)
   - Include additional parameters as needed.
4. Click **Add** to add the _InfluxDBBackendListenerClient_ implementation.

#### Configure FluentD

See the _[influxdb-plugin-fluent Readme](https://github.com/influxdata/influxdb-plugin-fluent)_ for details.