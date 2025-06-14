---
description: >-
  Risks related to process errors and inefficiencies of the general
  infrastructure.
---

# General Infrastructure (GIR)

<figure><img src="../../.gitbook/assets/DALL·E 2024-01-04 12.23.25 - A digital artwork depicting the risk of operational compromises in infrastructure. The image illustrates a complex system of machinery and control pan.png" alt=""><figcaption></figcaption></figure>

General infrastructure risks:


<table>
<thead>
<tr>
  <th width="98">ID</th>
  <th width="144">Risk Group</th>
  <th>Risk Vectors</th>
  <th>Risk Vector Description</th>
</tr></thead>
<tbody>
<tr>
  <td id="risk-gir-1">GIR1</td>
  <td>Infrastructure</td>
  <td>Not granular enough role-definitions for access control</td>
  <td>Internal employees and external hackers may gain access to too many systems if they manage to have a highly privileged role</td>
</tr>
<tr>
  <td id="risk-gir-2">GIR2</td>
  <td>Infrastructure</td>
  <td>Token lifetimes are too wide</td>
  <td>Authentication information does not expire timely and can be used later.</td>
</tr>
<tr>
  <td id="risk-gir-3">GIR3</td>
  <td>Infrastructure</td>
  <td>Fix versions on every deploy</td>
  <td>Downtime if a system needs to be just re-started if newest version is accidentally pulled</td>
</tr>
<tr>
  <td id="risk-gir-4">GIR4</td>
  <td>Process</td>
  <td>Insufficient monitoring/logging</td>
  <td>- Inability to learn from incidents<br>- Late detection of incidents<br>- insufficient automation to react to incidents</td>
</tr>
<tr>
  <td id="risk-gir-5">GIR5</td>
  <td>Process</td>
  <td>Insufficient off-boarding controls, e.g. by too many authentication mechanisms around.</td>
  <td>terminated employee can remain having access to systems and do harm</td>
</tr>
<tr>
  <td id="risk-gir-6">GIR6</td>
  <td>Process</td>
  <td>No password rotation</td>
  <td>- Leak of passwords<br>- brute force</td>
</tr>
<tr>
  <td id="risk-gir-7">GIR7</td>
  <td>Process</td>
  <td>Use of direct auth</td>
  <td>Authentication information does not expire timely and can be used later.</td>
</tr>
<tr>
  <td id="risk-gir-8">GIR8</td>
  <td>Process</td>
  <td>No Input validation</td>
  <td>Buffer overflow attacks</td>
</tr>
<tr>
  <td id="risk-gir-9">GIR9</td>
  <td>Infrastructure</td>
  <td>Failure to properly perform network segmentation</td>
  <td>No container/node should be openly accessible from the internet from all IP addresses. This increases the attack vector enormously</td>
</tr>
<tr>
  <td id="risk-gir-10">GIR10</td>
  <td>Infrastructure</td>
  <td>Lack of encrypted traffic between services and deployment scripts</td>
  <td>Anyone on the network can sniff out packages with secrets included, and may be able to steal passwords and tokens in this way</td>
</tr>
<tr>
  <td id="risk-gir-11">GIR11</td>
  <td>Infrastructure</td>
  <td>No separate tests and staging environments</td>
  <td>Improper change management and testing of software updates "in production"</td>
</tr>
<tr>
  <td id="risk-gir-12">GIR12</td>
  <td>Infrastructure</td>
  <td>General architectural flaws</td>
  <td>General risk category that can cause downtime, slashing, etc.<br>This includes, but is not limited to:<br>- Non-scalable deployments<br>- Use of tools not made for this purpose<br>- Lack of robustness/redundancy<br>- Bad change management<br>- Bad container isolation</td>
</tr>
<tr>
  <td id="risk-gir-13">GIR13</td>
  <td>Infrastructure</td>
  <td>High Blast radius of software bug in overall system</td>
  <td>A small error affects the whole system and all clients right away, instead of being caught early with limited effect on the whole system.</td>
</tr>
<tr>
  <td id="risk-gir-14">GIR14</td>
  <td>Infrastructure</td>
  <td>Low Infrastructure provider security</td>
  <td>Hacks through the apis of the infrastructure provider</td>
</tr>
<tr>
  <td id="risk-gir-15">GIR15</td>
  <td>Infrastructure</td>
  <td>CVE Monitoring</td>
  <td>Attack on the system suddenly possible once published</td>
</tr>
<tr>
  <td id="risk-gir-16">GIR16</td>
  <td>People</td>
  <td>Human error</td>
  <td>Anything a human can touch can go wrong</td>
</tr>
<tr>
  <td id="risk-gir-17">GIR17</td>
  <td>Process</td>
  <td>Use of non-hardened images</td>
  <td>Attack on the system using the weakest link of a given node/container</td>
</tr>
<tr>
  <td id="risk-gir-18">GIR18</td>
  <td>Process</td>
  <td>Insufficient change management mechanisms in place</td>
  <td>- Downtime on update<br>- Slow down in reaction time to incident</td>
</tr>
<tr>
  <td id="risk-gir-19">GIR19</td>
  <td>Process</td>
  <td>Lack of automation for deloyment</td>
  <td>- Downtime on update<br>- Slow down in reaction time to incident</td>
</tr>
<tr>
  <td id="risk-gir-20">GIR20</td>
  <td>Process</td>
  <td>Lack of testing (software and infrastructure)</td>
  <td>- Downtime on update<br>- Slow down in reaction time to incident</td>
</tr>
<tr>
  <td id="risk-gir-21">GIR21</td>
  <td>Process</td>
  <td>Lack of enforced code review</td>
  <td>- Downtime on update<br>- Slow down in reaction time to incident</td>
</tr>
<tr>
  <td id="risk-gir-22">GIR22</td>
  <td>Process</td>
  <td>Lack of Security training (password hygiene, phising attacks, ...)</td>
  <td>Employees spill secrets</td>
</tr>
<tr>
  <td id="risk-gir-23">GIR23</td>
  <td>Process</td>
  <td>Make-shift container orchestration procedures</td>
  <td>Failure when e.g. failover is actually needed to be performed</td>
</tr>
<tr>
  <td id="risk-gir-24">GIR24</td>
  <td>Software</td>
  <td>Third party software and vendors</td>
  <td>Suboptimal third-party software practices</td>
</tr>
<tr>
  <td id="risk-gir-25">GIR25</td>
  <td>People</td>
  <td>Centralized knowledge</td>
  <td>If the infrastructure knowledge is not shared across the team, this could lead to a heavy dependency on a single person</td>
</tr></tbody></table>
