---
coverY: 0
layout:
  cover:
    visible: false
    size: full
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# Prometheus Installation



{% hint style="danger" %}
**To experience a secure and practical monitoring service, I suggest you Check the previous section, which is about the prerequisites of Prometheus and Grafana.**
{% endhint %}

* <mark style="color:blue;">**Download latest version of Prometheus From**</mark>

[https://prometheus.io/download/](https://prometheus.io/download/)

```
Wget https://github.com/prometheus/prometheus/releases/download/v2.48.1/prometheus-2.48.1.linux-amd64.tar.gz
```

* <mark style="color:blue;">**Untar Our Files**</mark>

```
tar xvfz prometheus-2.48.1.linux-amd64.tar.gz
```

* <mark style="color:blue;">**CD into the folder**</mark>

```
cd prometheus-2.48.1.linux-amd64
```

* <mark style="color:blue;">**Run the File**</mark>

```
./prometheus --config.file=prometheus.yml
```

* [x] Prometheus should now be running.🎁🎁🎁

You can Check it at http://\[your ip address]:9090

{% hint style="info" %}
The Prometheus installation has been completed. The only issue is that, when the system restarts or we puse the proccess , the Prometheus service also stops. To resolve this problem, we need to place the Prometheus files in the “bin” directory
{% endhint %}



<mark style="color:orange;">**Start Prometheus as a Service**</mark>

* <mark style="color:blue;">**Stop Prometheus process and copy the new files to bin folder**</mark>

```
cp -r . /usr/local/bin/prometheus
```

* <mark style="color:blue;">**Create a file called prometheus.service**</mark>

```
sudo  vi /etc/systemd/system/prometheus.service
```

* <mark style="color:blue;">**Add the script and save**</mark>

```
[Unit]
Description=Prometheus Service
After=network.target

[Service]
Type=simple
ExecStart=/usr/local/bin/prometheus/prometheus --config.file=/usr/local/bin/prometheus/prometheus.yml

[Install]
WantedBy=multi-user.target

```

* <mark style="color:blue;">**Now start and check the service is running.**</mark>

```
sudo service prometheus start
sudo service prometheus status
```
