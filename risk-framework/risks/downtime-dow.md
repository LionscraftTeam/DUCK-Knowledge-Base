---
description: Connectivity issues leading to reduced rewards.
---

# Downtime (DOW)

<figure><img src="../../.gitbook/assets/DALL·E 2024-01-04 12.21.33 - A digital artwork that captures the concept of downtime risk in a technological context. The image features a large, central clock with its hands froz (1).png" alt=""><figcaption></figcaption></figure>

Downtime Risks:


<table>
<thead>
<tr>
<th width="109">ID</th>
<th width="141">Risk Group</th>
<th>Risk Vectors</th>
<th>Risk Vector Description</th>
</tr></thead>
<tbody>
<tr>
  <td id="risk-dow-1">DOW1</td>
  <td>Infrastructure</td>
  <td>External: Operational Failure of Cloud Service Provider</td>
  <td>Cloud Downtime, malfunction</td>
</tr>
<tr>
  <td id="risk-dow-2">DOW2</td>
  <td>Infrastructure</td>
  <td>Operational Failure of own bare metal set-up due to malfunction software</td>
  <td>Malfunction of software (e.g. validator client or third party software) leads to downtime</td>
</tr>
<tr>
  <td id="risk-dow-3">DOW3</td>
  <td>Infrastructure</td>
  <td>Operational Failure of own bare metal set-up due to malfunction hardware</td>
  <td>Malfunction of hardware (e.g. physical network, computer system, CPU, RAM) leads to downtime</td>
</tr>
<tr>
  <td id="risk-dow-4">DOW4</td>
  <td>Infrastructure</td>
  <td>External: Operational Failure of own bare metal set-up due to people (ManMade)</td>
  <td>Employees are responsible for the downtime event (accidentally or intentionally)</td>
</tr>
<tr>
  <td id="risk-dow-5">DOW5</td>
  <td>Infrastructure</td>
  <td>External: Operational Failure of own bare metal set-up due to natural causes</td>
  <td>A natural event (e.g. earthquake, flood, hurricane,...) leads to an downtime</td>
</tr>
<tr>
  <td id="risk-dow-6">DOW6</td>
  <td>Infrastructure</td>
  <td>Failure to design for high availability</td>
  <td>Having too few beacon nodes relative to validator clients, leading to:<br>- opportunity costs<br>- slashing on some networks</td>
</tr>
<tr>
  <td id="risk-dow-7">DOW7</td>
  <td>Infrastructure</td>
  <td>External: Internet connectivity</td>
  <td>Loss of infrastructure network connection due to:<br>- Sudden cloud outage<br>- Sudden internet failure in on-premise machines<br>- Accidental firewall change locks out access.</td>
</tr>
<tr>
  <td id="risk-dow-8">DOW8</td>
  <td>Infrastructure</td>
  <td>External: Power supply</td>
  <td>Power Breakdown</td>
</tr>
<tr>
  <td id="risk-dow-9">DOW9</td>
  <td>Infrastructure</td>
  <td>External: Power supply</td>
  <td>Volatile power supply damages infrastructure</td>
</tr>
<tr>
  <td id="risk-dow-10">DOW10</td>
  <td>Infrastructure</td>
  <td>External: DDOS attack</td>
  <td>Systems unresponsive, slowed down, and compromized due to buffer/stack overflow</td>
</tr>
<tr>
  <td id="risk-dow-11">DOW11</td>
  <td>Software</td>
  <td>Software Bug in the Validator Client</td>
  <td id="risk-dow-ntime or accidental interpretation of dishonest behavior">DOWntime or accidental interpretation of dishonest behavior</td>
</tr>
<tr>
  <td id="risk-dow-12">DOW12</td>
  <td>Software</td>
  <td>Software Bug in the Validator Client (Intentional or accidental) through software update</td>
  <td>New versions of a validator client that may cause errors that lead to downtime<br>(Supply chain attack)</td>
</tr>
<tr>
  <td id="risk-dow-13">DOW13</td>
  <td>Software</td>
  <td>Software Bug in the Validator Client through software customization</td>
  <td><br>New versions of a validator client may cause errors that lead to downtime</td>
</tr>
<tr>
  <td id="risk-dow-14">DOW14</td>
  <td>Software</td>
  <td>Software Bug in third party software</td>
  <td><br>Third party software failure can lead to downtime of the whole system</td>
</tr>
<tr>
  <td id="risk-dow-15">DOW15</td>
  <td>Software</td>
  <td>Latency / Failure of relays</td>
  <td>Latency / Failure of relays </td>
</tr>
<tr>
  <td id="risk-dow-16">DOW16</td>
  <td>People</td>
  <td>Malicious Internal Employee (intentionally causes operational failure)</td>
  <td>An employee having too privileged access</td>
</tr>
<tr>
  <td id="risk-dow-17">DOW17</td>
  <td>People</td>
  <td>Malicious Ex-Employee intentionally causes a downtime incident</td>
  <td>A Ex-Employee can still have access to the system when his acces is not blocked or removed</td>
</tr>
<tr>
  <td id="risk-dow-18">DOW18</td>
  <td>People</td>
  <td>Malicious External Hacker (intentionally causes operational failure)</td>
  <td>A hacker may find a way to overload the<br>system or shut parts of it down manually.</td>
</tr>
<tr>
  <td id="risk-dow-19">DOW19</td>
  <td>Software</td>
  <td>Running outdated validator software</td>
  <td>The node operator os not updating its validator software</td>
</tr>
<tr>
  <td id="risk-dow-20">DOW20</td>
  <td>Software</td>
  <td>Validator client update incompatible with IT system</td>
  <td>System downtime after validator client update caused by incompatibility</td>
</tr></tbody></table>
