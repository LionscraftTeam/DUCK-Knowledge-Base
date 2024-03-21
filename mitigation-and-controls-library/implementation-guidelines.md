# Implementation Guidelines

## Infrastructure Guidelines

### :vertical\_traffic\_light: Validator Node Security Checklist

<table><thead><tr><th width="265">Concern</th><th>Solution</th></tr></thead><tbody><tr><td>Secure the root account</td><td><pre><code>ssh -i secure_key username@staking.node.ip.address
sudo useradd -m -s /bin/bash ethereum
sudo passwd ethereum
sudo usermod -aG sudo ethereum
</code></pre></td></tr><tr><td>Connect with SSH Keys Only</td><td><p></p><p>The basic rules of hardening SSH are:</p><ul><li>No password for SSH access (use private key)</li><li>Don't allow root to SSH (the appropriate users should SSH in, then <code>su</code> or <code>sudo</code>)</li><li>Use <code>sudo</code> for users so commands are logged</li><li>Log unauthorized login attempts (and consider software to block/ban users who try to access your server too many times, like fail2ban)</li><li>Lock down SSH to only the ip range your require (if you feel like it)</li></ul><pre><code>sudo vim /etc/ssh/sshd_config
PasswordAuthentication no
sudo sshd -t
sudo systemctl restart sshd
</code></pre></td></tr><tr><td>Harden SSH on a random port</td><td><pre><code>sudo vim /etc/ssh/sshd_config
Port &#x3C;your random port number>
sudo sshd -t
sudo systemctl restart sshd
</code></pre></td></tr><tr><td>Setup 2-FA for SSH</td><td><a href="https://github.com/google/google-authenticator-libpam">https://github.com/google/google-authenticator-libpam</a></td></tr><tr><td>Secure the Shared Memory</td><td><p></p><p>Memory encryption is enabled on the following instances:</p><ul><li>Instances with AWS Graviton processors. AWS Graviton2, AWS Graviton3, and AWS Graviton3E support always-on memory encryption. The encryption keys are securely generated within the host system, do not leave the host system, and are destroyed when the host is rebooted or powered down. For more information, see <a href="http://aws.amazon.com/ec2/graviton">AWS Graviton Processors.</a></li><li>Instances with 3rd generation Intel Xeon Scalable processors (Ice Lake), such as M6i instances, and 4th generation Intel Xeon Scalable processors (Sapphire Rapids), such as M7i instances. These processors support always-on memory encryption using Intel Total Memory Encryption (TME).</li><li>Instances with 3rd generation AMD EPYC processors (Milan), such as M6a instances, and 4th generation AMD EPYC processors (Genoa), such as M7a instances. These processors support always-on memory encryption using AMD Secure Memory Encryption (SME). Instances with 3rd generation AMD EPYC processors (Milan) also support AMD Secure Encrypted Virtualization-Secure Nested Paging (SEV-SNP).</li></ul></td></tr><tr><td>Setup a firewall</td><td>The standard UFW firewall can be used to control network access to your node.</td></tr><tr><td>Setup port forwarding on my router</td><td>Setup VPN and Trusted Locations Access in all Firewalls</td></tr><tr><td>Setup intrusion-prevention monitoring</td><td>Install <a href="https://github.com/fail2ban/fail2ban">https://github.com/fail2ban/fail2ban</a></td></tr><tr><td>Whitelist your local machine in the ufw firewall</td><td>Setup VPN and Trusted Locations Access in all Firewalls</td></tr><tr><td>Whitelisted your local machine in Fail2ban</td><td><a href="https://github.com/fail2ban/fail2ban/wiki">https://github.com/fail2ban/fail2ban/wiki</a></td></tr><tr><td>Verify the listening ports</td><td><code>netstat -tulpn</code></td></tr></tbody></table>

### :vertical\_traffic\_light: Validator Node Maintenance and Best Practices Checklist

<table data-full-width="false"><thead><tr><th>Concern</th><th>Solution</th></tr></thead><tbody><tr><td>Enabled automatic OS patching</td><td>Use <a href="https://docs.aws.amazon.com/systems-manager/latest/userguide/patch-manager.html">AWS Patch Manager</a>.</td></tr><tr><td>Setup chrony or other NTP time sync service</td><td><a href="https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/set-time.html">https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/set-time.html</a></td></tr><tr><td>Setup Prometheus and Grafana Monitoring/Alerts/Dashboard</td><td>Refer to the <a data-mention href="implementation-guidelines.md#monitoring-guidelines">#monitoring-guidelines</a></td></tr><tr><td>Understand how to handle a power outage</td><td>In case of power outage, you want your validator machine to restart as soon as power is available. In the BIOS settings, change the <strong>Restore on AC / Power Loss</strong> or <strong>After Power Loss</strong> setting to always on. Better yet, install an Uninterruptable Power Supply (UPS).<br><br>Use different Availability Zones of your Cloud provider.</td></tr><tr><td>Understand how to migrate consensus clients</td><td>Refer to the consensus client docs.</td></tr><tr><td>Understand how to voluntary exit</td><td><a href="https://docs.prylabs.network/docs/wallet/exiting-a-validator">https://docs.prylabs.network/docs/wallet/exiting-a-validator</a></td></tr><tr><td>Understand important directory locations</td><td>Refer to the mainnet guide.</td></tr><tr><td>Networking</td><td>Assign static internal IPs to both your validator node and daily laptop/PC. This is useful in conjunction with ufw and Fail2ban's whitelisting feature. Typically, this can be configured in your router's settings. Consult your router's manual for instructions.</td></tr><tr><td>Power Outage</td><td>In case of power outage, you want your validator machine to restart as soon as power is available. In the BIOS settings, change the <strong>Restore on AC / Power Loss</strong> or <strong>After Power Loss</strong> setting to always on. Better yet, install an Uninterruptable Power Supply (UPS).</td></tr><tr><td>Clear the bash history</td><td><p>When pressing the up-arrow key, you can see prior commands which may contain sensitive data. To clear this, run the following:</p><p><code>shred -u ~/.bash_history &#x26;&#x26; touch ~/.bash_history</code></p></td></tr></tbody></table>

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

According to the [Google SRE handbook](https://landing.google.com/sre/sre-book/chapters/monitoring-distributed-systems/#xref\_monitoring\_golden-signals), if you can only measure four metrics of your user-facing system, focus on these four.

This method is similar to the RED method, but it includes saturation.

* **Latency -** Time taken to serve a request
* **Traffic -** How much demand is placed on your system
* **Errors -** Rate of requests that are failing
* **Saturation -** How “full” your system is

### Dashboard management maturity model <a href="#dashboard-management-maturity-model" id="dashboard-management-maturity-model"></a>

_Dashboard management maturity_ refers to how well-designed and efficient your dashboard ecosystem is. We recommend periodically reviewing your dashboard setup to gauge where you are and how you can improve.

You should have optimised your dashboard management use with a consistent and thoughtful strategy. It requires maintenance, but the results are worth it.

* Actively reducing sprawl.
  * Regularly review existing dashboards to make sure they are still relevant.
  * Only approved dashboards added to master dashboard list.
  * Tracking dashboard use. If you’re an Enterprise user, you can take advantage of [Usage insights](https://grafana.com/docs/grafana/latest/dashboards/assess-dashboard-usage/).
* Consistency by design.
* Use scripting libraries to generate dashboards, ensure consistency in pattern and style.
  * grafonnet (Jsonnet)
  * grafanalib (Python)
* No editing in the browser. Dashboard viewers change views with variables.
* Browsing for dashboards is the exception, not the rule.
* Perform experimentation and testing in a separate Grafana instance dedicated to that purpose, not your production instance. When a dashboard in the test environment is proven useful, then add that dashboard to your main Grafana instance.

#### Before you begin <a href="#before-you-begin" id="before-you-begin"></a>

Here are some principles to consider before you create a dashboard.

**A dashboard should tell a story or answer a question**

What story are you trying to tell with your dashboard? Try to create a logical progression of data, such as large to small or general to specific. What is the goal for this dashboard? (Hint: If the dashboard doesn’t have a goal, then ask yourself if you really need the dashboard.)

Keep your graphs simple and focused on answering the question that you are asking. For example, if your question is “which servers are in trouble?”, then maybe you don’t need to show all the server data. Just show data for the ones in trouble.

**Dashboards should reduce cognitive load, not add to it**

_Cognitive load_ is basically how hard you need to think about something in order to figure it out. Make your dashboard easy to interpret. Other users and future you (when you’re trying to figure out what broke at 2AM) will appreciate it.

Ask yourself:

* Can I tell what exactly each graph represents? Is it obvious, or do I have to think about it?
* If I show this to someone else, how long will it take them to figure it out? Will they get lost?

**Have a monitoring strategy**

It’s easy to make new dashboards. It’s harder to optimize dashboard creation and adhere to a plan, but it’s worth it. This strategy should govern both your overall dashboard scheme and enforce consistency in individual dashboard design.

Refer to [Common observability strategies](https://grafana.com/docs/grafana/latest/dashboards/build-dashboards/best-practices/#common-observability-strategies) and [Dashboard management maturity levels](https://grafana.com/docs/grafana/latest/dashboards/build-dashboards/best-practices/#dashboard-management-maturity-model) for more information.

**Write it down**

Once you have a strategy or design guidelines, write them down to help maintain consistency over time. Check out this [Wikimedia runbook example](https://wikitech.wikimedia.org/wiki/Performance/Runbook/Grafana\_best\_practices).

#### Best practices to follow <a href="#best-practices-to-follow" id="best-practices-to-follow"></a>

* When creating a new dashboard, make sure it has a meaningful name.
  * If you are creating a dashboard to play or experiment, then put the word `TEST` or `TMP` in the name.
  * Consider including your name or initials in the dashboard name or as a tag so that people know who owns the dashboard.
  * Remove temporary experiment dashboards when you are done with them.
* If you create many related dashboards, think about how to cross-reference them for easy navigation. Refer to [Best practices for managing dashboards](https://grafana.com/docs/grafana/latest/dashboards/build-dashboards/best-practices/#best-practices-for-managing-dashboards) for more information.
* Grafana retrieves data from a data source. A basic understanding of [data sources](https://grafana.com/docs/grafana/latest/datasources/) in general and your specific is important.
* Avoid unnecessary dashboard refreshing to reduce the load on the network or backend. For example, if your data changes every hour, then you don’t need to set the dashboard refresh rate to 30 seconds.
* Use the left and right Y-axes when displaying time series with different units or ranges.
* Add documentation to dashboards and panels.
  * To add documentation to a dashboard, add a [Text panel visualization](https://grafana.com/docs/grafana/latest/panels-visualizations/visualizations/text/) to the dashboard. Record things like the purpose of the dashboard, useful resource links, and any instructions users might need to interact with the dashboard. Check out this [Wikimedia example](https://grafana.wikimedia.org/d/000000066/resourceloader?orgId=1).
  * To add documentation to a panel, edit the panel settings and add a description. Any text you add will appear if you hover your cursor over the small `i` in the top left corner of the panel.
* Reuse your dashboards and enforce consistency by using [templates and variables](https://grafana.com/docs/grafana/latest/dashboards/variables/).
* Be careful with stacking graph data. The visualizations can be misleading, and hide important data. We recommend turning it off in most cases.

### Best practices for managing dashboards <a href="#best-practices-for-managing-dashboards" id="best-practices-for-managing-dashboards"></a>

This page outlines some best practices to follow when managing Grafana dashboards.

#### Before you begin <a href="#before-you-begin-1" id="before-you-begin-1"></a>

Here are some principles to consider before you start managing dashboards.

**Strategic observability**

There are several common observability strategies. You should research them and decide whether one of them works for you or if you want to come up with your own. Either way, have a plan, write it down, and stick to it.

Adapt your strategy to changing needs as necessary.

**Maturity level**

What is your dashboard maturity level? Analyze your current dashboard setup and compare it to the Dashboard management maturity model. Understanding where you are can help you decide how to get to where you want to be.

#### Best practices to follow <a href="#best-practices-to-follow-1" id="best-practices-to-follow-1"></a>

* Avoid dashboard sprawl, meaning the uncontrolled growth of dashboards. Dashboard sprawl negatively affects time to find the right dashboard. Duplicating dashboards and changing “one thing” (worse: keeping original tags) is the easiest kind of sprawl.
  * Periodically review the dashboards and remove unnecessary ones.
  * If you create a temporary dashboard, perhaps to test something, prefix the name with `TEST:` . Delete the dashboard when you are finished.
* Copying dashboards with no significant changes is not a good idea.
  * You miss out on updates to the original dashboard, such as documentation changes, bug fixes, or additions to metrics.
  * In many cases copies are being made to simply customize the view by setting template parameters. This should instead be done by maintaining a link to the master dashboard and customizing the view with [URL parameters](https://grafana.com/docs/grafana/latest/panels-visualizations/configure-data-links/#data-link-variables).
* When you must copy a dashboard, clearly rename it and _do not_ copy the dashboard tags. Tags are important metadata for dashboards that are used during search. Copying tags can result in false matches.
* Maintain a dashboard of dashboards or cross-reference dashboards. This can be done in several ways:
  * Create dashboard links, panel, or data links. Links can go to other dashboards or to external systems. For more information, refer to [Manage dashboard links](https://grafana.com/docs/grafana/latest/dashboards/build-dashboards/manage-dashboard-links/).
  * Add a [Dashboard list panel](https://grafana.com/docs/grafana/latest/panels-visualizations/visualizations/dashboard-list/). You can then customize what you see by doing tag or folder searches.
  * Add a [Text panel](https://grafana.com/docs/grafana/latest/panels-visualizations/visualizations/text/) and use markdown to customize the display.

Source: Grafana Docs







