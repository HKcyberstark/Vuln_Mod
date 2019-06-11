# Vuln_Mod
An opensource vulnerability assessment module documenting the integration of OpenVAS with elastic stack using VulnWhisperer.

## Overview
Vulnerability assessment tool used for Vulnerability Testing, is an assesment performed to evaluate the security risks in the software system in order to reduce the probability of a threat.

Detecting the vulnerabilities is not the best efficient step, reviewing and acting on the detected vulnerability counts as the best security practice.  

With efficient integration of open source tools, we could build an open source vulnerability module, that can help in detecting, reviewing and analysing the vulnerability data in the environment.

![Vuln_Mod architecture](https://user-images.githubusercontent.com/40884455/59201047-1f865f80-8bcc-11e9-9005-67977a45f243.JPG)

### OpenVAS
The [Open Vulnerability Assessment System](http://www.openvas.org/) (OpenVAS) is a vulnerability scanner maintained and distributed by Greenbone Networks. It is intended to be an all-in-one vulnerability scanner with a variety of built-in tests and a Web interface designed to make setting up and running vulnerability scans fast and easy while providing a high level of user configurability.

### Elastic stack
[Elastic Stack](https://www.elastic.co/products/) is a software suite (Logstash, Elasticsearch, Kibana) used to collect, parse, index, store, search, and present log data. It provides a web front-end that gives a high-level dashboard view of events that allows for advanced analytics and data mining deep into your store of event data.

### VulnWhisperer 
[VulnWhisperer](https://github.com/HASecuritySolutions/VulnWhisperer) is a vulnerability management tool and report aggregator. VulnWhisperer will pull all the reports from the different Vulnerability scanners and create a file with a unique filename for each one, using that data later to sync and feed into Logstash.

## System Requirements
Below are the basic system requirements for dev environment.  Higher memory and hard drive space depends on the number of scans and data load

**Server 1: OpenVAS and Vulnwhisperer**  
- 2 CPUs
- 3GB of memory
- 30GB of hard drive (this depends on number of scans and how much data you will retain)

**Server 2: Elastic Stack**
- 2 CPUs
- 4GB of memory
- 50 GB of hard drive (this depends on number of scans and how much data you will retain)

## Installation
We would be Installing the above Open source tools in minimal install of [CentOS](https://www.centos.org/download/).
step by step installation guides are docuumented in [installation-docs](https://github.com/HKcyberstark/Vuln_Mod/tree/master/installation-docs) section of this repository.

## How it works
When the VulnWhisperer is configured for OpenVAS and is running, It pulls out the available scan reports from the OpenVAS and parses with json format. The data is stored locally [/opt/VulnWhisperer/data/openvas/] and processed by configured logstash.  the Kibana visualisation provided by Vulnwhisperer team provides out of the box analytical visualisation on the scanned data.

Logstash and Kibana Visualisation configurations are available in [config](https://github.com/HKcyberstark/Vuln_Mod/tree/master/config) section of this repository. 

## Screenshot examples

![0](https://user-images.githubusercontent.com/40884455/59238334-4bd3c780-8c30-11e9-920e-22d190860fd1.jpeg)

## Credits and References
The module is an integration of OpenVas Vulnerability assesment tool wih Elastic stack using Vulnwhisperer. credits to all the brains behind these open source projects.

[Vulnwhisperer](https://github.com/HASecuritySolutions/VulnWhisperer)

[Elastic stack](https://github.com/HASecuritySolutions/VulnWhisperer)

[OpenVAS](http://www.openvas.org/)
