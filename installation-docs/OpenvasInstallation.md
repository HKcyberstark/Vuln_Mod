### Installing Pre requirements
1. OpenVas requires SELinux to be disabled.
 
`sed -i 's/=enforcing/=disabled/' /etc/selinux/config`

2. Open the necessary port for OpenVAS web interface right away

`firewall-cmd --zone=public --add-port=9392/tcp --permanent

firewall-cmd –reload`

3. install the wget package and net tools

`yum -y install wget net-tools`

4. Install/configure the repository from Atomic Corp (use default answers when adding keys for the Atomic Corp repository).

`wget -q -O - https://updates.atomicorp.com/installers/atomic | sh`

*Note: If you have issues with ‘updates’ in the wget URL above, using either ‘www’ or ‘www6’ works instead. For example,*

`wget -q -O – https://www.atomicorp.com/installers/atomic | sh

wget -q -O – https://www6.atomicorp.com/installers/atomic | sh`

### Installing/Configuring OpenVAS (GVM)
1. Install OpenVAS (GVM) and related dependencies. (This will install over 300MB of dependencies so be patient.)

`yum -y install greenbone-vulnerability-manager`

2. When yum completes, uncomment the following 2 unixsocket-related lines in the /etc/redis.conf file

`unixsocket /tmp/redis.sock

unixsocketperm 700`

*Note: You can also below ‘sed’ command to uncomment the unixsocket line directly.*

`sed -i '/^#.*unixsocket/s/^# //' /etc/redis.conf`

3. Enable and restart the redis service

`systemctl enable redis && systemctl restart redis`

4. **Here we go –  Run a command ‘openvas-setup’ and accept rsync as your default**

`openvas-setup`

![openvas-setup](https://user-images.githubusercontent.com/40884455/59202328-ce2b9f80-8bce-11e9-850f-b5a4501d5a52.JPG)

*Note: This can take a while so be patient. It is downloading GBs worth of data. If youface any issues with downloads just run openvas-setup again. Also, just a reminder that rsync uses TCP port 873 so you may have to allow it outbound in your egress firewall rules and/or configure it to work with your proxy server.*
 
Once openvas-setup completes and some keys are generated, you will receive the prompts asking to “Allow connections from any IP?”  you can accept the default of ‘yes’ by simply pressing enter assuming you want to access the web interface from any IP address. You can change your username (I stayed with ‘admin’) and type in the password (twice) that you want to use to access the web interface.
 
*Note: The system will build/rebuild the NVT cache. This step can also take a bit of time so be patient. Rebuilding NVT is followed with a message that you can now access the interface*

5. Run the below Two commands to start gsad on port 9392 as the package states.

`echo 'OPTIONS="--listen=0.0.0.0 --port=9392"' > /etc/sysconfig/gsad

systemctl start gsad`

Now OpnVas Web interface can be accessed with https://[your IP address]:9392

![web interface](https://user-images.githubusercontent.com/40884455/59202425-029f5b80-8bcf-11e9-8ba6-f3345ddaa41f.JPG)

You will receive a security prompt regarding the certificate since it is self-signed, but after that you should be able to login.

### Feed Updates.
Any vulnerability assessment tool is efficient only when the environment is tested with latest vulnerability feeds. Thus, if your feeds are out-of-date, your scans are not going to reflect the true nature of the environment because you are not testing for the most recently discovered vulnerabilities. From the web interface, you can check the status of your feeds anytime via **Extras -> Feed Status**

The feeds don’t update automatically by default. You could update them manually or you can configure the feeds to update automatically via [cron jobs](https://www.thegeekdiary.com/centos-rhel-begginners-guide-to-cron/)

![cron job](https://user-images.githubusercontent.com/40884455/59202495-2d89af80-8bcf-11e9-9ab1-d942425e09c4.JPG)
 
### Configure PDF reports with OpenVAS
Install additional texlive packages for CentOS 7

`yum -y install texlive-collection-fontsrecommended texlive-collection-latexrecommended texlive-changepage texlive-titlesec`

The following steps were found on [Blogpost](http://miotramemoria.blogspot.com/2014/08/centos-7-openvas-pdf-reports.html).Openvas 7 pdf reports don't work in centOS 7 due to changes in texlive packaging in RHEL7, the resulting pdf file has 0 bytes size, to solve this problem do this: 
(We need to install the comment.sty and other dependencies that are already packaged.)
 
![pdf report](https://user-images.githubusercontent.com/40884455/59202548-4befab00-8bcf-11e9-94fe-e3c51f17a7c7.JPG)

OpenVas is installed and configured. Further found this [video](https://www.youtube.com/watch?v=-2vjsHmq3ak) to be very useful for OpenVas Administration.