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
wget https://github.com/prometheus/prometheus/releases/download/v2.48.1/prometheus-2.48.1.linux-amd64.tar.gz
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
sudo systemctl enable prometheus
sudo service prometheus status
```



{% hint style="danger" %}
The installation of Nginx is complete, but it is completely exposed to attacks via the network and the internet. We will take further actions to secure the Prometheus server.
{% endhint %}



<mark style="color:orange;">**Step \_1**</mark>

<mark style="color:orange;">**Implemet Web authentication**</mark>

```
sudo sh -c "echo -n 'USERNAME:' >> /etc/nginx/.htpasswd"
sudo apt update
sudo apt install apache2-utils
```

<mark style="color:blue;">**The option “-c” allows you to create a new file.**</mark>

```
sudo htpasswd -c /etc/nginx/.htpasswd vahid
```

```
sudo nano /etc/nginx/sites-enabled/default

auth_basic "Restricted Content";
auth_basic_user_file /etc/nginx/.htpasswd;

```

```
sudo systemctl restart nginx
```



<mark style="color:orange;">**Step\_2**</mark>

<mark style="color:orange;">**limit access to port 9090 and only accept requests from the HTTPS port**</mark>&#x20;

```
sudo nano /etc/nginx/sites-enabled/default
```

```
proxy_pass https://127.0.0.1:9090;
```

```
sudo systemctl restart nginx
```

[**Phase II**](https://en.wikipedia.org/wiki/Phase\_II)

```
systemctl status prometheus

nano /etc/systemd/system/prometheus.service
```

Add the following switch and allowed IP ADDRESSES  in ‘Exexstart’ line:\
(Allow the Grafana server at IP address 192.168.2.2 to have access to the Prometheus server)

```
--web.listen-address=127.0.0.1:9090,192.168.2.2:9090
```

```
systemctl daemon-reload
systemctl restart prometheus
```
