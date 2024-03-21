---
description: Blueprint provided by kiln
---

# Large Node Operator



<figure><img src="../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

## Stakeholder Overview

<table data-full-width="false"><thead><tr><th width="149">Group</th><th width="154">Stakeholder</th><th width="277">Level of Engagement</th><th>Comms. Channels</th></tr></thead><tbody><tr><td>Institutional Stakers</td><td>Enterprise customers (eg Bitpanda)</td><td><p>Communicating the <a href="https://www.kiln.fi/reports">monthly performance</a></p><p> </p><p>Communication if there is a major outage that might affect the SLAs</p></td><td><p>Slack, fortnightly meeting</p><p> </p><p>Status page: <a href="https://status.kiln.fi/">https://status.kiln.fi/</a></p></td></tr><tr><td>Service Partners</td><td>Liquid staking protocol customers (eg Lido)</td><td>Communication with them on any outage, communication of postmortems (not just with the LST protocol but also with other validators where relevant)<br><br>Performing tests for them (eg <a href="https://www.kiln.fi/post/learnings-from-running-web3signer-at-scale-on-holesky">holesky web3 signer scale test</a>)</td><td>Telegram</td></tr><tr><td>Software Providers</td><td>3rd party software teams (eg Web3 signer, clients Teku, Prysm)</td><td>Share bugs and issues</td><td>Telegram, Github issues</td></tr><tr><td>Auditors</td><td>Auditors (eg., Quantstamp)</td><td>Share any outage and postmortem. Share architectural designs/changes</td><td>Slack</td></tr><tr><td>Communities</td><td>Ethereum foundation</td><td>Organizing talks, sharing some feedback on the latest hot topics (upgrades, <a href="https://ethresear.ch/t/empirical-analysis-of-the-impact-of-block-delays-on-the-consensus-layer/17888">now timing games</a>)</td><td>Telegram</td></tr></tbody></table>

## Best Practices

1. Try not to have more than one active channel per stakeholder.
2. Define [incident response plan](https://docs.google.com/document/d/1K3GEbRFTyNy2zKkUJwEYFzkzFJu2IGwc/edit)[s](https://docs.google.com/document/d/1K3GEbRFTyNy2zKkUJwEYFzkzFJu2IGwc/edit) to be prepared for potential incidents.
3. Aim to follow the [Google SRE incident management practices](https://sre.google/workbook/incident-response/).&#x20;
4. Focus on declaring incidents fast/easily, stop the bleeding, and try to reduce over-communication.

## Hot Topics

1. Continuous training of people on incident management
2. Ensuring you have a good on-call rotation&#x20;
3. Reduce over-communication

## Tools in Use

1. For incident communications [incident.io](https://incident.io/) is used. It helps streamline internal resolution, helps write the post-mortem, and publishes to [https://status.kiln.fi/](https://status.kiln.fi/)
2. [Worknet](https://www.worknet.ai/) as a slack bot to do bulk messaging to groups of customer slack channels.
3. Standard tools like [grafana](https://grafana.com/) & [pagerduty](https://www.pagerduty.com/)

## Effectiveness Metrics

1. Are SLAs being met? (ETH target is 99% uptime, [like coinbase](https://www.coinbase.com/cloud/discover/insights-analysis/when-less-is-more), so there is typically enough buffer)
2. Are the customers happy with the level of communication?
