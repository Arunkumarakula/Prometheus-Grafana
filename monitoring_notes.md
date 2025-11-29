Monitoring means continuously watching your servers, websites, applications, and systems to know:

Are they running correctly?

Are they slow?

Are they using too much CPU/RAM?

Are they down?

Are there errors?

* We use monitoring to:
  - Detect Problems Early: Server down, Website unreachable, SSL certificate expired, Disk full

 1. Infrastructure Monitoring: Monitors servers/VMs - CPU, RAM, Disk, Network

    Tools:
    - Node Exporter + Prometheus
    - Nagios
    - Datadog Infrastructure

  2. Application Monitoring: Monitors APIs & applications - API response time, Error rate, Request count

     Tools:
     - Prometheus + Grafana
     - Datadog APM

  3. Website/Uptime Monitoring: Checks Website is UP, Website status code,SSL expiry, Response time

     Tools:
     - Blackbox Exporter + Prometheus
     - StatusCake

  4. Log Monitoring: Reads logs and analyzes Errors, Exceptions, Slow queries, Crashes

     Tools:
     - ELK Stack (Elasticsearch + Logstash + Kibana)
     - Filebeat

  5. Container & Docker Monitoring: Tracks Container CPU, Container memory, Running containers

     Tools:
     - cAdvisor
     - Prometheus
     - Grafana
     - Datadog Containers

------------------------------------------------------------------------------------------------------------------------------------------------------------

Prometheus: Prometheus is an open-source monitoring tool used to collect, store, and analyze metrics from servers, websites, applications, and containers.

- collects metrics from exporters

- stores metrics in its own time-series database (TSDB)

- lets you query metrics using PromQL (PromQL is the query language of Prometheus)

- triggers alerts using alert rules

- provides data to Grafana for dashboards

* Why Prometheus is used:

   1. To collect metrics: Prometheus collects data like CPU usage, RAM usage, Disk usage, Website status, API response time, SSL expiry, Container stats

   2. To store time-series data: Prometheus has its own database called TSDB (Time Series Database). 
      Every metric is stored with: value, timestamp, labels

      Example metric: node_cpu_seconds_total{instance="server1", mode="idle"} 12345

   3. To trigger alerts: Prometheus checks alert rules such as Server down, Website unreachable, Disk 90% full, SSL expires in 7 days, Alerts go to Email.

* How Prometheus Works:
   - Prometheus reads prometheus.yml
   - It sees the targets (node exporter, blackbox exporter, APIs…)
   - It pulls (scrapes) metrics from them every 15s
   - It stores the data in TSDB
   - It checks alert rules (CPU, website down)
   - It shows raw metrics in its UI or sends data to Grafana

------------------------------------------------------------------------------------------------------------------------------------------------------------

What is an Exporter:

- An Exporter is a small program that collects metrics from a system and exposes them to Prometheus.
- Prometheus does NOT collect metrics by itself.
- It pulls (scrapes) metrics from exporters.

Tools:
 - Node Exporter: collects syetem metrics like CPU, RAM, Disk, Network of a server
 - cadvisor: collects Docker container metrics
 - Blackbox: Website up/down, SSL, HTTP status

------------------------------------------------------------------------------------------------------------------------------------------------------------

Difference between Logs and Metrics:

 - Metrics are Numbers Lightweight Stored in Prometheus and used for graphs/alerts Collected every 15s.
 - Logs are text Heavy Stored in Elasticsearch/Logstash Used for debugging errors Generated every event

Example:

Metric → CPU = 45%, RAM = 60%

Log → User login failed: invalid password

------------------------------------------------------------------------------------------------------------------------------------------------------------

Blackbox Exporter: Blackbox Exporter is a Prometheus exporter used to monitor external endpoints like Websites, APIs, Ports, DNS, Ping (ICMP)
                  - It checks whether something is reachable from the outside

------------------------------------------------------------------------------------------------------------------------------------------------------------

Grafana: Grafana is an open-source data visualization and monitoring platform that allows you to create interactive dashboards, analyze metrics, and set up
         alerts by connecting to data sources like Prometheus.
