# Grafana Installation

###

{% hint style="info" %}
**To experience a secure and practical monitoring service, I suggest you Check the previous section, which is about the prerequisites of Prometheus and Grafana.**
{% endhint %}

### <mark style="color:orange;">Installing the Grafana</mark>



<mark style="color:green;">**Steps for Installing Grafan**</mark>

* <mark style="color:blue;">**Update the package info**</mark>&#x20;

```
sudo apt-get install -y apt-transport-https
```

```
sudo apt-get install -y software-properties-common wget
```

```
wget -q -O - https://packages.grafana.com/gpg.key | sudo apt-key add -
```

* Add stable repository of Grafana -

```
echo "deb https://packages.grafana.com/enterprise/deb stable main" | sudo tee -a /etc/apt/sources.list.d/grafana.list
```

* <mark style="color:blue;">**Update repository and Install Grafana**</mark>

```
sudo apt-get update
```

```
sudo apt-get install grafana-enterprise
```

* Start the `Grafana Server`&#x20;

```
sudo systemctl daemon-reload
sudo systemctl start grafana-server
sudo systemctl status grafana-server
```

* Configure Grafana to run automatically at boot&#x20;

```
sudo systemctl enable grafana-server.service
```

{% hint style="danger" %}
Make sure port 3000 is open in the firewall.
{% endhint %}

Done✔✔✔&#x20;

&#x20;

* You can open the Grafana Dashboard using `http://localhost:3000/login`



<figure><img src=".gitbook/assets/grafana-dashboard-login.webp" alt=""><figcaption></figcaption></figure>



{% hint style="warning" %}
The default login **Username: Password** for accessing the Grafana dashboard is **admin: admin**
{% endhint %}

Enjoy 🎁🎁🎁



{% hint style="info" %}
In the next tutorial,  We See how to work with the Grafana dashboard and get metric.
{% endhint %}

##
