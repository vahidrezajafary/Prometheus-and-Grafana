# Grafana Dashboard





{% hint style="success" %}
In the previous step, we saw how to install Grafana. In this step, we will see how to connect it to Prometheus and set up the Grafana dashboard.
{% endhint %}

* <mark style="color:blue;">**Add Prometheus Inside Grafana Dashboard As Datasource**</mark>&#x20;

<figure><img src=".gitbook/assets/data so.png" alt=""><figcaption><p><mark style="color:blue;"><strong>Grafana Dashboard create data source</strong></mark></p></figcaption></figure>

<figure><img src=".gitbook/assets/data-pr.png" alt=""><figcaption><p><mark style="color:blue;"><strong>Prometheus as preferred data source</strong></mark></p></figcaption></figure>

<figure><img src=".gitbook/assets/dataa-pro-2.png" alt=""><figcaption><p><mark style="color:blue;"><strong>Enter the hostname or ip address of prometheus server e.g. http://localhost:9090</strong></mark></p></figcaption></figure>

<figure><img src=".gitbook/assets/test.png" alt=""><figcaption><p><mark style="color:blue;"><strong>Save and test prometheus datasource</strong></mark></p></figcaption></figure>





{% hint style="success" %}
**After settings the data source we can import pre-existing opensource dashboard from** [**Grafana Labs**](https://grafana.com/grafana/dashboards/) **using the Dashboard ID.**
{% endhint %}

* <mark style="color:orange;">**Goto**</mark> [**Grafana Dashboard**](https://grafana.com/grafana/dashboards/) <mark style="color:orange;">**and search for What you looking for.( e.g. CPU Usage)**</mark>



<figure><img src=".gitbook/assets/import-0.png" alt=""><figcaption></figcaption></figure>



* <mark style="color:blue;">**Click on the result and copy the Dashboard ID or URL**</mark>

<figure><img src=".gitbook/assets/cpu.png" alt=""><figcaption></figcaption></figure>

* <mark style="color:blue;">**Goto Back to Grafana, Dashboard => New => Import**</mark>

Enter the Dashboard ID or past URL

<figure><img src=".gitbook/assets/import.png" alt=""><figcaption></figcaption></figure>



<figure><img src=".gitbook/assets/import-2.png" alt=""><figcaption></figcaption></figure>



<mark style="background-color:green;">**Done**</mark> ✔✔✔
