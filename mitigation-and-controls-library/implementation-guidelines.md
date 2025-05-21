# Implementation Guidelines

## Infrastructure Guidelines

### :vertical\_traffic\_light: Validator Node Security Checklist

<table><thead><tr><th width="265">Concern</th><th>Risk</th><th>Solution</th></tr></thead><tbody><tr><td>Secure the root account</td><td>KEC7<br>GIR1<br>GIR16<br>SLS9<br>DOW16<br>DOW17</td><td><pre><code>ssh -i secure_key username@staking.node.ip.address
sudo useradd -m -s /bin/bash ethereum
sudo passwd ethereum
sudo usermod -aG sudo ethereum
</code></pre></td></tr><tr><td>Connect with SSH Keys Only</td><td>GIR7<br>GIR22<br>SLS12<br>SLS13<br>DOW16<br>DOW17</td><td><p></p><p>The basic rules of hardening SSH are:</p><ul><li>No password for SSH access (use private key)</li><li>Don't allow root to SSH (the appropriate users should SSH in, then <code>su</code> or <code>sudo</code>)</li><li>Use <code>sudo</code> for users so commands are logged</li><li>Log unauthorized login attempts (and consider software to block/ban users who try to access your server too many times, like fail2ban)</li><li>Lock down SSH to only the ip range your require (if you feel like it)</li></ul><pre><code>sudo vim /etc/ssh/sshd_config
PasswordAuthentication no
sudo sshd -t
sudo systemctl restart sshd
</code></pre></td></tr><tr><td>Harden SSH on a random port</td><td>GIR9</td><td><pre><code>sudo vim /etc/ssh/sshd_config
Port &#x3C;your random port number>
sudo sshd -t
sudo systemctl restart sshd
</code></pre></td></tr><tr><td>Setup 2-FA for SSH</td><td>GIR7</td><td><a href="https://github.com/google/google-authenticator-libpam">https://github.com/google/google-authenticator-libpam</a></td></tr><tr><td>Secure the Shared Memory</td><td>GIR8<br>GIR12<br>GIR15<br>GIR17<br>GIR24<br>KEC7</td><td><p></p><p>Memory encryption is enabled on the following instances:</p><ul><li>Instances with AWS Graviton processors. AWS Graviton2, AWS Graviton3, and AWS Graviton3E support always-on memory encryption. The encryption keys are securely generated within the host system, do not leave the host system, and are destroyed when the host is rebooted or powered down. For more information, see <a href="http://aws.amazon.com/ec2/graviton">AWS Graviton Processors.</a></li><li>Instances with 3rd generation Intel Xeon Scalable processors (Ice Lake), such as M6i instances, and 4th generation Intel Xeon Scalable processors (Sapphire Rapids), such as M7i instances. These processors support always-on memory encryption using Intel Total Memory Encryption (TME).</li><li>Instances with 3rd generation AMD EPYC processors (Milan), such as M6a instances, and 4th generation AMD EPYC processors (Genoa), such as M7a instances. These processors support always-on memory encryption using AMD Secure Memory Encryption (SME). Instances with 3rd generation AMD EPYC processors (Milan) also support AMD Secure Encrypted Virtualization-Secure Nested Paging (SEV-SNP).</li></ul></td></tr><tr><td>Setup a firewall</td><td>GIR9</td><td>The standard UFW firewall can be used to control network access to your node.</td></tr><tr><td>Setup port forwarding on my router</td><td>GIR9</td><td>Setup VPN and Trusted Locations Access in all Firewalls</td></tr><tr><td>Setup intrusion-prevention monitoring</td><td>GIR9</td><td>Install <a href="https://github.com/fail2ban/fail2ban">https://github.com/fail2ban/fail2ban</a></td></tr><tr><td>Whitelist your local machine in the ufw firewall</td><td>GIR9<br>GIR14</td><td>Setup VPN and Trusted Locations Access in all Firewalls</td></tr><tr><td>Whitelisted your local machine in Fail2ban</td><td>GIR9</td><td><a href="https://github.com/fail2ban/fail2ban/wiki">https://github.com/fail2ban/fail2ban/wiki</a></td></tr><tr><td>Verify the listening ports</td><td>GIR9</td><td><code>netstat -tulpn</code></td></tr></tbody></table>

### :vertical\_traffic\_light: Validator Node Maintenance and Best Practices Checklist

<table data-full-width="false"><thead><tr><th>Concern</th><th>Risk</th><th>Solution</th></tr></thead><tbody><tr><td>Enabled automatic OS patching or define an internal process to test and apply patches</td><td>GIR15<br>GIR17</td><td>Example: Use <a href="https://docs.aws.amazon.com/systems-manager/latest/userguide/patch-manager.html">AWS Patch Manager</a> but keep in mind AWS doesn't test patches before making them available in Patch Manager. It is essential to test every change to ensure smooth functionality. </td></tr><tr><td>Setup chrony or other NTP time sync service</td><td>GIR24</td><td><a href="https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/set-time.html">https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/set-time.html</a></td></tr><tr><td>Setup Prometheus and Grafana Monitoring/Alerts/Dashboard</td><td>SLS17</td><td>Refer to the <a data-mention href="implementation-guidelines.md#monitoring-guidelines">#monitoring-guidelines</a></td></tr><tr><td>Understand how to handle a power outage</td><td>DOW8<br>DOW9</td><td>In case of power outage, you want your validator machine to restart as soon as power is available. In the BIOS settings, change the <strong>Restore on AC / Power Loss</strong> or <strong>After Power Loss</strong> setting to always on. Better yet, install an Uninterruptable Power Supply (UPS).<br><br>Use different Availability Zones of your Cloud provider.</td></tr><tr><td>Understand how to migrate consensus clients</td><td>DOW13</td><td>Refer to the consensus client docs.</td></tr><tr><td>Understand how to voluntary exit</td><td>SPS1</td><td><a href="https://docs.prylabs.network/docs/wallet/exiting-a-validator">https://docs.prylabs.network/docs/wallet/exiting-a-validator</a></td></tr><tr><td>Understand important directory locations</td><td>SLS5</td><td>Refer to the mainnet guide.</td></tr><tr><td>Networking</td><td>GIR9<br>GIR10</td><td>Assign static internal IPs to both your validator node and daily/work laptop/PC. This is useful in conjunction with ufw and Fail2ban's whitelisting feature. Typically, this can be configured in your router's settings. Consult your router's manual for instructions.</td></tr><tr><td>Power Outage</td><td>DOW8<br>DOW9</td><td>In case of power outage, you want your validator machine to restart as soon as power is available. In the BIOS settings, change the <strong>Restore on AC / Power Loss</strong> or <strong>After Power Loss</strong> setting to always on. Better yet, install an Uninterruptable Power Supply (UPS).</td></tr><tr><td>Clear the bash history</td><td>KEC3</td><td><p>When pressing the up-arrow key, you can see prior commands which may contain sensitive data. To clear this, run the following:</p><p><code>shred -u ~/.bash_history &#x26;&#x26; touch ~/.bash_history</code></p></td></tr></tbody></table>

##

## Monitoring Guidelines

When you have a lot to monitor, like a server farm, you need a strategy to decide what is important enough to monitor:

A logical strategy allows you to make uniform dashboards and scale your observability platform more easily.

#### Guidelines for usage <a href="#guidelines-for-usage" id="guidelines-for-usage"></a>

* The USE method tells you how happy your machines are, the RED method tells you how happy your users are.
* USE reports on causes of issues.
* RED reports on user experience and is more likely to report symptoms of problems.
* The best practice of alerting is to alert on symptoms rather than causes, so alerting should be done on RED dashboards.

#### USE method <a href="#use-method" id="use-method"></a>

USE stands for:

* **Utilization -** Percent time the resource is busy, such as node CPU usage
* **Saturation -** Amount of work a resource has to do, often queue length or node load
* **Errors -** Count of error events

![](https://www.brendangregg.com/USEmethod/usemethod\_flow.png)

This method is best for hardware resources in infrastructure, such as CPU, memory, and network devices. For more information, refer to [The USE Method](http://www.brendangregg.com/usemethod.html).

Example to show the **user CPU usage**:\
\
Requirements:&#x20;

* [nodeexporter](https://github.com/prometheus/node\_exporter) installed on machine
* [grafana](https://github.com/grafana/grafana) + [prometheus](https://github.com/prometheus/prometheus)
* setup prometheus config to scrape metrices of nodeexporter

Define Queries in your Grafana Dashboard:

Query a:

```promql
sum by(instance) (irate(node_cpu_seconds_total{instance="$node",job="$job", mode="user"}[$__rate_interval])) / on(instance) group_left sum by (instance)((irate(node_cpu_seconds_total{instance="$node",job="$job"}[$__rate_interval])))
```

Query b:

```promql
sum by(instance) (irate(node_cpu_seconds_total{instance="$node",job="$job", mode="idle"}[$__rate_interval])) / on(instance) group_left sum by (instance)((irate(node_cpu_seconds_total{instance="$node",job="$job"}[$__rate_interval])))
```

Set Unit in Standard options in the panel settings to Percent (0.0-1.0).

#### RED method <a href="#red-method" id="red-method"></a>

RED stands for:

* **Rate -** Requests per second
* **Errors -** Number of requests that are failing
* **Duration -** Amount of time these requests take, distribution of latency measurements

This method is most applicable to services, especially a microservices environment. For each of your services, instrument the code to expose these metrics for each component. RED dashboards are good for alerting and SLAs. A well-designed RED dashboard is a proxy for user experience.

Example:

Set up your own [ethereum-validators-monitoring](https://github.com/lidofinance/ethereum-validators-monitoring) and define Alerts.

#### The Four Golden Signals (4GS) <a href="#the-four-golden-signals" id="the-four-golden-signals"></a>

The [Google SRE handbook](https://landing.google.com/sre/sre-book/chapters/monitoring-distributed-systems/#xref\_monitoring\_golden-signals) suggests that if you can only measure four metrics of your user-facing system, focus on these four.

This method is similar to the RED method, but it includes saturation.

* **Latency -** Time taken to serve a request
* **Traffic -** How much demand is placed on your system
* **Errors -** Rate of requests that are failing
* **Saturation -** How “full” your system is

#### Grafana dashboard management

The [best practices for Grafana dashboards](https://grafana.com/docs/grafana/latest/dashboards/build-dashboards/best-practices/) offer a wealth of advice on selecting and managing information dashboards to provide useful actionable information.
