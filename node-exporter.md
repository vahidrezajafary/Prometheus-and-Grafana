# Node Exporter



{% hint style="info" %}
Node exporter is responsible for fetching the statistics from various hardware and virtual resources in the format which Prometheus can understand and with the help of the prometheus server those statistics can be exposed on port **9100**.

In this tutorial, we will install the node exporter on a separate server as well as locally on the Prometheus server.
{% endhint %}



<mark style="color:orange;">**install the Node Exporter on our Prometheus server and configure it as a Service.**</mark>

* We will download the node exporter binary from the Prometheus downloads page at [https://prometheus.io/download/#node\_exporter](https://prometheus.io/download/#node\_exporter)



* <mark style="color:blue;">**Download Prometheus Node Exporter Binary and run**</mark>

```
wget https://github.com/prometheus/node_exporter/releases/download/v1.7.0/node_exporter-1.7.0.linux-amd64.tar.gz
```

* <mark style="color:blue;">**Untar the File**</mark>

```
tar xvfz node_exporter-1.7.0.linux-amd64.tar.gz
```

* <mark style="color:blue;">**Copy File to the**</mark>** **<mark style="color:orange;">**/usr/local/bin/ folder**</mark>

```
cp node_exporter-1.7.0.l.linux-amd64/node_exporter /usr/local/bin/node_exporter
```

* <mark style="color:blue;">**Configure Prometheus Node Exporter as a Service, Create a file called node-exporter.service**</mark>

```
sudo vi /etc/systemd/system/node-exporter.service
```

* <mark style="color:blue;">**Add the script and save**</mark>

```
[Unit]
Description=Prometheus Node Exporter Service
After=network.target

[Service]
Type=simple
ExecStart=/usr/local/bin/node_exporter

[Install]
WantedBy=multi-user.target

```

* <mark style="color:blue;">**Now start and check the service is running.**</mark>

```
sudo systemctl daemon-reload
sudo service node-exporter start
sudo service node-exporter status
```

{% hint style="danger" %}
Make sure port 3000 is open in the firewall.
{% endhint %}

<mark style="color:orange;">**Node exporter will now be running on http://\[your domain or ip]:9100/metrics**</mark>

Now Add the new scrape config for the new node exporter.

Scroll down to the bottom file and add a new scrape config

```
sudo vi /usr/local/bin/prometheus/prometheus.yml 
```

```
global:
   scrape_interval: 15s

scrape_configs:
   - job_name: node
     static_configs:
    - targets: ['localhost:9100']
```



{% hint style="danger" %}
&#x20;if you want to add _node exporter_ for any remote server then you need to define `scrap_configs` with `target` hosts inside the YAML configuration.


{% endhint %}



```
global:
   scrape_interval: 15s

scrape_configs:
   - job_name: node
     static_configs:
        - targets: ['localhost:9100','Remote_Server_IP_ADD:9100'] 
```



* <mark style="color:blue;">**Finally restart the prometheus service and Done.**</mark>

```
sudo service prometheus restart
sudo service prometheus status
```



<mark style="background-color:green;">**Enjoy**</mark> ✔✔✔
