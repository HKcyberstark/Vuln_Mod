## ElasticSearch
1. Install the Elastic repository and its GPG key

`rpm --import https://packages.elastic.co/GPG-KEY-elasticsearch`

`vi /etc/yum.repos.d/elastic.repo`

```
[elasticsearch-7.x]
name=Elasticsearch repository for 7.x packages
baseurl=https://artifacts.elastic.co/packages/7.x/yum
gpgcheck=1
gpgkey=https://artifacts.elastic.co/GPG-KEY-elasticsearch
enabled=1
autorefresh=1
type=rpm-md
```

2. Install the Elasticsearch package

`yum install elasticsearch-7.1.1`

3. Enable and start the Elasticsearch service

```
systemctl daemon-reload
systemctl enable elasticsearch.service
systemctl start elasticsearch.service
```

## Kibana
1. Install the Kibana package

`yum install kibana-7.1.1`

*Optional : Kibana will only listen on the loopback interface (localhost) by default. To set up Kibana to listen on all interfaces, edit the file /etc/kibana/kibana.yml uncommenting the setting server.host*
`server.host: "0.0.0.0"`

3. Enable and start the Kibana service

```
systemctl daemon-reload
systemctl enable kibana.service
systemctl start kibana.service
```

*Optional Disable the Elasticsearch repository:It is recommended that the Elasticsearch repository be disabled in order to prevent an upgrade to a newer Elastic Stack version*

`sed -i "s/^enabled=1/enabled=0/" /etc/yum.repos.d/elastic.repo`

## Logstash
1. Install the Logstash package

`yum install logstash-7.1.1`

2. get the Logstash configuration file [config](https://github.com/HKcyberstark/Vuln_Mod/tree/master/config) section of this repository and place it in /etc/logstash/config/

3. Enable and start the logstash service

```
systemctl daemon-reload
systemctl enable logstash.service
systemctl start logstash.service
```

VulnWhisperer team provides out of the box visualisation which can be imported into Kibana. Visualisation config is available in [config](https://github.com/HKcyberstark/Vuln_Mod/tree/master/config) section of this repository.