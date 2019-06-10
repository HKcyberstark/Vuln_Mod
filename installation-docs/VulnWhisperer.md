## Installation
1. git clone https://github.com/HASecuritySolutions/VulnWhisperer.git 
2. Install python libraries requirements

`pip install -r /path/to/VulnWhisperer/requirements.txt`

`cd /path/to/VulnWhisperer`

`python setup.py install`

*(Optional) If using a proxy, add proxy URL as environment variable to PATH*

*export HTTP_PROXY=http://example.com:8080*

*export HTTPS_PROXY=http://example.com:8080*

3. Configure Ini file to collect OpnVas scan results. edit openVas section as below in the frameworks_example.ini available in the configs folder inside Vulnwhisperer clone.

*change enabled to true, provide username and passoword of openVAS*

[openvas]

enabled = true

hostname = localhost

port = 4000

username = exampleuser

password = examplepass

write_path=/opt/VulnWhisperer/data/openvas/

db_path=/opt/VulnWhisperer/data/database

verbose=true


4. Run VulnWhisperer

`vuln_whisperer -c configs/frameworks_example.ini -s openvas`

Next, you'll need to setup your logstash config and import the visualizations into Kibana.Logstash and Kibana configurations are provided in config section of this repository.
