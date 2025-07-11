---
description: Losing access to critical system components.
---

# Key Compromises (KEC)

<figure><img src="../../.gitbook/assets/DALL·E 2024-01-04 12.22.34 - A digital artwork depicting the risk of infrastructure access compromises. The image shows a large, intricate network of pipes and wires, symbolizing .png" alt=""><figcaption></figcaption></figure>

## Validator Key Custody Risk


<table>
<thead>
<tr>
<th width="105">ID</th>
<th width="140">Risk Group</th>
<th width="226">Risk Vectors</th>
<th>Risk Vector Description</th>
</tr></thead>
<tbody>
<tr>
  <td id="risk-kec-1">KEC1</td>
  <td>Infrastructure</td>
  <td>Failure to use vault system</td>
  <td>No audit trail and controlled access to secrets</td>
</tr>
<tr>
  <td id="risk-kec-2">KEC2</td>
  <td>People</td>
  <td>Stolen / Lost Signing Keys (malicious internal employee)</td>
  <td>Malicious employee deletes or steals the signing keys</td>
</tr>
<tr>
  <td id="risk-kec-3">KEC3</td>
  <td>People</td>
  <td>Stolen / Lost Signing Keys (malicious internal employee)</td>
  <td>Malicious employee gets access to the unencrypted signing keys</td>
</tr>
<tr>
  <td id="risk-kec-4">KEC4</td>
  <td>People</td>
  <td>Stolen / Lost Signing Keys (External Hacker)</td>
  <td>Malicious external hacker deletes signing keys</td>
</tr>
<tr>
  <td id="risk-kec-5">KEC5</td>
  <td>People</td>
  <td>Stolen / Lost Signing Keys (External Hacker)</td>
  <td>Stealing the signing key from the unencrypted memory of the Web3Signer, even if keys are encrypted at rest in a vault</td>
</tr>
<tr>
  <td id="risk-kec-6">KEC6</td>
  <td>Process</td>
  <td>Loss of Signing Keys (Operational Failure)</td>
  <td>Signing keys are lost in an operational process</td>
</tr>
<tr>
  <td id="risk-kec-7">KEC7</td>
  <td>Process</td>
  <td>Privilege escalation mechanisms not prevented</td>
  <td>Someone with access to one service/node can increase their privileges and do more harm on further nodes.</td>
</tr>
<tr>
  <td id="risk-kec-8">KEC8</td>
  <td>Infrastructure</td>
  <td>Failure to protect infrastructure against physical access</td>
  <td>Someone who gains physical access to a server can have access to locally exposed ports and can access the software API</td>
</tr></tbody></table>

## Withdrawal Key Custody Risk


<table>
<thead>
<tr>
<th width="107">ID</th>
<th width="134">Risk Group</th>
<th>Risk Vectors</th>
<th>Risk Vector Description</th>
</tr></thead>
<tbody>
<tr>
  <td id="risk-kec-9">KEC9</td>
  <td>Process</td>
  <td>Loss of Withdrawal Keys (Operational Failure)</td>
  <td>Loss of Withdrawal Keys (Operational Failure)</td>
</tr>
<tr>
  <td id="risk-kec-10">KEC10</td>
  <td>People</td>
  <td>Stolen Withdrawal Keys (Internal Employee)</td>
  <td>Stolen Withdrawal Keys (Internal Employee)</td>
</tr>
<tr>
  <td id="risk-kec-11">KEC11</td>
  <td>People</td>
  <td>Stolen Withdrawal Keys (External Hacker)</td>
  <td>Stolen Withdrawal Keys (External Hacker)</td>
</tr></tbody></table>
