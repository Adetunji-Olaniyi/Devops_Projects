Monitor Linux Server using Prometheus Node Exporter
Introduction
Monitoring a Linux server is essential for ensuring system health and performance.

Prometheus Node Exporter is a powerful tool that collects hardware and operating system metrics, providing deep insights into our server's state per time. This project will guide you through installing and configuring Prometheus Node Exporter on a Linux server and monitoring it with Prometheus.

Objectives
Install and configure Prometheus Node Exporter on a Linux server.
Integrate Node Exporter with Prometheus for metric collection.
Explore system metrics collected by Node Exporter.
Set up basic queries in Prometheus for real-time monitoring.
Optionally configure alerts for key metrics.
Prerequisites
Linux Server: A running Linux server with sudo privileges.
Prometheus Instance: A working Prometheus setup (local or remote).
Network Access: Ensure Prometheus can connect to the Linux server on port 9100.
Tools: Terminal access to the Linux server, Prometheus UI access, and a text editor for authoring configuration files.
Tasks Outline
Install Prometheus Node Exporter on the Linux server.
Start and enable Node Exporter as a service.
Configure Prometheus to scrape metrics from Node Exporter.
Verify and query Node Exporter metrics in Prometheus.
Explore and analyze the collected metrics on the Prometheus UI.
Project Tasks
Task 1 - Install Prometheus Node Exporter
Download the latest Node Exporter binary from the Prometheus GitHub releases page:

I will be spining up Lib=nux server on AWS to install prometheus and node exporter.

Prometheus

Connect to the server using Gitbash and run the commands below:

curl -LO https://github.com/prometheus/node_exporter/releases/download/v1.10.2/node_exporter-1.10.2.linux-amd64.tar.gz

NodeExporterDownload

Extract the downloaded tarball:

tar -xvf node_exporter-1.10.2.linux-amd64.tar.gz

ExtractDownloads

Move the binary to a directory in your PATH:

sudo mv node_exporter-1.10.2.linux-amd64/node_exporter /usr/local/bin/

Movedthebinary

Task 2 - Start and Enable Node Exporter as a Service
Create a systemd service file for Node Exporter by running the command below:

sudo nano /etc/systemd/system/node_exporter.service

Systemdservices

Add the following content to the file:

contentsystemdfile

contentadded

Reload systemd and start the Node Exporter service using the following commands:

sudo systemctl daemon-reload

sudo systemctl start node_exporter

sudo systemctl enable node_exporter

reloadsystemd

Verify that Node Exporter is running with this command:

sudo systemctl status node_exporter

NodeExporterRunning

Confirm Node Exporter is accessible by visiting http://3.215.22.86:9100/metrics in a web browser. If you are using your computer, is localhost

NodeExportAccessible

Task 3 - Configure Prometheus to Scrape Metrics from Node Exporter
Open the Prometheus configuration file (prometheus.yml):

vim /etc/prometheus/prometheus.yml

PrometheusConfigFile

Add a new scrape job for Node Exporter:

ExporterNode

ScrapeJobAdded

Save the file and restart Prometheus to apply the changes:

sudo systemctl restart prometheus

Task 4 - Verify and Query Node Exporter Metrics in Prometheus
Access the Prometheus web interface (e.g., http://3.222.251.1:9100)

PremethusInterface

Run a test query to verify Node Exporter metrics:

Example: node_cpu_seconds_total to view CPU usage.
cpuusage

Check the "Targets" page in Prometheus to confirm the Node Exporter target is listed and "UP."

Task 5 - Explore and Analyze Metrics
Use the Prometheus query interface to explore key Node Exporter metrics:

node_memory_MemAvailable_bytes for Available Memory.
node_filesystem_avail_bytes for Available Disk Space.
node_network_receive_bytes_total: Network Bytes Received.
usage

Create basic time-series graphs using Prometheus expressions (PromQL):

Example: rate(node_cpu_seconds_total[5m]) to analyze CPU usage over the last 5 minutes.
Optionally, set up alert rules for critical metrics like high CPU usage or low disk space.

Conclusion
In this project, you installed and configured Prometheus Node Exporter on a Linux server, integrated it with Prometheus, and explored collected metrics. These skills provide a strong foundation for monitoring server health and performance, and you can now extend this setup by adding advanced visualization tool like Grafana.

END.