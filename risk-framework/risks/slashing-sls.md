---
description: Performing slashable actions leading to penalties.
---

# Slashing (SLS)

<figure><img src="../../.gitbook/assets/DALL·E 2024-01-04 12.20.23 - A digital artwork visualizing the concept of slashing in Ethereum. The image features a stylized Ethereum logo, fractured or slashed, to represent the (1).png" alt=""><figcaption></figcaption></figure>

Slashing Risks:


<table>
<thead>
<tr>
<th width="96">ID</th>
<th width="138">Risk Group</th>
<th width="232">Risk Vectors</th>
<th>Risk Vector Description</th>
</tr></thead>
<tbody>
<tr>
  <td id="risk-sls-1">SLS1</td>
  <td>Infrastructure</td>
  <td>Operational Failure: Single validator signs two different blocks</td>
  <td>Single node signs two different blocks, e.g. failure in setting up the anti-slashing mechanism (e.g. no lokal anti-slashing database disabled or deleted) or failure in the validator migration process.</td>
</tr>
<tr>
  <td id="risk-sls-2">SLS2</td>
  <td>Infrastructure</td>
  <td>Operational Failure: Shutting down validator only temporarily</td>
  <td>Validator shuts (temporary) down. System spins up a new validator with the same key</td>
</tr>
<tr>
  <td id="risk-sls-3">SLS3</td>
  <td>Infrastructure</td>
  <td>Operational Failure: Validator keys are used on 2 different validators</td>
  <td>System takes the same keys twice from the key database and deploys them on two different validators.</td>
</tr>
<tr>
  <td id="risk-sls-4">SLS4</td>
  <td>Infrastructure</td>
  <td>Operational Failure: Failure in setting up the anti-slashing mechanisms correctly</td>
  <td>Failure in setting up the anti-slashing mechanisms correctly (e.g. Web3Signer has no slashing protection enabled, no database, database only in memory and not on disk, 2 or several copies of Web3Signer, slashing databse can be deleted)</td>
</tr>
<tr>
  <td id="risk-sls-5">SLS5</td>
  <td>Infrastructure</td>
  <td>Double key usage in the CI/CD pipeline</td>
  <td>Usage of same key within different environments causing a slashing</td>
</tr>
<tr>
  <td id="risk-sls-6">SLS6</td>
  <td>Software</td>
  <td>Software Bug (e.g. Validator Client) (Intentional or accidentional) through update</td>
  <td>New versions of a validator client that may cause errors that lead to slashing<br>Supply chain attack</td>
</tr>
<tr>
  <td id="risk-sls-7">SLS7</td>
  <td>Software</td>
  <td>Software Bug (e.g. Validator Client) through software customization</td>
  <td><br>New versions of a validator client may cause errors that lead to slashing</td>
</tr>
<tr>
  <td id="risk-sls-8">SLS8</td>
  <td>People</td>
  <td>Malicious Internal Employee intentionally causes operational failure via his given user rights</td>
  <td>Anything that an internal employee has access to is at risk of being exploited to sabotage the operation resulting in a slashing incident.</td>
</tr>
<tr>
  <td id="risk-sls-9">SLS9</td>
  <td>People</td>
  <td>Malicious Internal Employee intentionally causes operational failure via privilege escalation</td>
  <td>A malicious internal employee can get additional rights via through privileges escalation.</td>
</tr>
<tr>
  <td id="risk-sls-10">SLS10</td>
  <td>People</td>
  <td>Malicious Ex-Employee intentionally causes a slashing incident</td>
  <td>A Ex-Employee can still have access to the system when his acces is not blocked or removed</td>
</tr>
<tr>
  <td id="risk-sls-11">SLS11</td>
  <td>People</td>
  <td>Malicious External Hacker intentionally causes slashing incident</td>
  <td>Malicious External Hacker gets system access through absence of or weak cyber security standards</td>
</tr>
<tr>
  <td id="risk-sls-12">SLS12</td>
  <td>People</td>
  <td>Malicious External Hacker intentionally causes slashing incident</td>
  <td>Malicious External Hacker gets external network access to the system</td>
</tr>
<tr>
  <td id="risk-sls-13">SLS13</td>
  <td>People</td>
  <td>Malicious External Hacker intentionally causes operational failure through authentication access</td>
  <td>Malicious External Hacker can get access through by-passing or brut-forcing authentication systems</td>
</tr>
<tr>
  <td id="risk-sls-14">SLS14</td>
  <td>Process</td>
  <td>Operational Failure: Incorrect implementation of the failover mechanism: Failover system comes unexpectedly online</td>
  <td>If the failover does not ensure that old system is not still alive in some way or is using a stale version of the anti-slashing database, e.g.: failover system starts accidentally although primary system is not down</td>
</tr>
<tr>
  <td id="risk-sls-15">SLS15</td>
  <td>Process</td>
  <td>Operational Failure: Incorrect implementation of the failover mechanism: Primary system comes unexpectedly back online</td>
  <td>If the failover does not ensure that old system is not still alive in some way or is using a stale version of the anti-slashing database, e.g.: failover system starts (manually / automatically) because primary system is down and primary system comes back online</td>
</tr>
<tr>
  <td id="risk-sls-16">SLS16</td>
  <td>Process</td>
  <td>Operational Failure: Slashing monitoring does not prevent system shut down</td>
  <td>Slashing events keep ongoing on because no slashing monitoring system in place</td>
</tr>
<tr>
  <td id="risk-sls-17">SLS17</td>
  <td>Process</td>
  <td>Operational Failure: Slashing monitoring ignores alerts</td>
  <td>Monitoring is in place, but slashing events keep ongoing on because alerts are not monitored</td>
</tr>
<tr>
  <td id="risk-sls-18">SLS18</td>
  <td>Process</td>
  <td>Operational Failure: Slashing monitoring does not shut down the validators</td>
  <td>Slashing keeps going on because system fails to automatically shut down after alerts</td>
</tr></tbody></table>
