---
description: Losing access to critical system components.
---

# Key Compromises (KEC)

<figure><img src="../../.gitbook/assets/DALL·E 2024-01-04 12.22.34 - A digital artwork depicting the risk of infrastructure access compromises. The image shows a large, intricate network of pipes and wires, symbolizing .png" alt=""><figcaption></figcaption></figure>

## Validator Key Custody Risk

<table><thead><tr><th width="105">ID</th><th width="140">Risk Group</th><th width="226">Risk Vectors</th><th>Risk Vector Description</th></tr></thead><tbody><tr><td>KEC1</td><td>Infrastructure</td><td>Failure to use vault system</td><td>No audit trail and controlled access to secrets</td></tr><tr><td>KEC2</td><td>People</td><td>Stolen / Lost Signing Keys (malicious internal employee)</td><td>Malicious employee deletes the signing keys</td></tr><tr><td>KEC3</td><td>People</td><td>Stolen / Lost Signing Keys (malicious internal employee)</td><td>Malicious employee gets access to the unencrypted signing keys</td></tr><tr><td>KEC4</td><td>People</td><td>Stolen / Lost Signing Keys (External Hacker)</td><td>Malicious external hacker deletes signing keys</td></tr><tr><td>KEC5</td><td>People</td><td>Stolen / Lost Signing Keys (External Hacker)</td><td>Stealing the signing key from the unencrypted memory of the Web3Signer, even if keys are encrypted at rest in a vault</td></tr><tr><td>KEC6</td><td>Process</td><td>Loss of Validator Keys (Operational Failure)</td><td>Validator keys are lost in an operational process</td></tr><tr><td>KEC7</td><td>Process</td><td>Privilege escalation mechanisms not prevented</td><td>Someone with access to one service/node can increase their privileges and do more harm on further nodes.</td></tr></tbody></table>

## Withdrawal Key Custody Risk

<table><thead><tr><th width="107">ID</th><th width="134">Risk Group</th><th>Risk Vectors</th><th>Risk Vector Description</th></tr></thead><tbody><tr><td>KEC8</td><td>Process</td><td>Loss of Withdrawal Keys (Operational Failure)</td><td>Loss of Withdrawal Keys (Operational Failure)</td></tr><tr><td>KEC9</td><td>People</td><td>Stolen Withdrawal Keys (Internal Employee)</td><td>Stolen Withdrawal Keys (Internal Employee)</td></tr><tr><td>KEC10</td><td>People</td><td>Stolen Withdrawal Keys (External Hacker)</td><td>Stolen Withdrawal Keys (External Hacker)</td></tr></tbody></table>
