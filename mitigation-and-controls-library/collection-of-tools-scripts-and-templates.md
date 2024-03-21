# Collection of Tools, Scripts & Templates

## Ethereum-Specific

| Tools                          | Description                                                                                                                         | Purpose                     | Links                                                                                                                                                                                   |
| ------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------- | --------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Doppelbuster                   | This tool operates independently from the Ethereum validator client, providing an extra layer of protection against double signing. | prevent double signing      | [https://github.com/SimplyStaking/DoppelBuster](https://github.com/SimplyStaking/DoppelBuster)                                                                                          |
| ethereum-validators-monitoring | Ethereum validators monitoring bot aimed to keep track of the validators performance                                                | monitoring + alerts         | [https://github.com/lidofinance/ethereum-validators-monitoring](https://github.com/lidofinance/ethereum-validators-monitoring)                                                          |
| vouch + dirk                   | Splits your validator keys and replaces the standard validator client software.                                                     | multi-node validator client | <p><a href="https://github.com/attestantio/vouch">https://github.com/attestantio/vouch</a><br><a href="https://github.com/attestantio/dirk">https://github.com/attestantio/dirk</a></p> |
| web3signer                     | Can sign on multiple platforms using private keys stored in an external vault, or encrypted on a disk                               | validator client            | [https://github.com/Consensys/web3signer](https://github.com/Consensys/web3signer)                                                                                                      |

## Inventory tracking

| Tools              | Description                                                                               | Purpose   | Links                                                                                                                                                                                                                 |
| ------------------ | ----------------------------------------------------------------------------------------- | --------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Internal Wiki      | Keep an updated inventory list, including the server type, purpose, and responsible team. | tracking  | [https://www.jetbrains.com/help/youtrack/server/knowledge-base.html](https://www.jetbrains.com/help/youtrack/server/knowledge-base.html)                                                                              |
| arp-scan, arpwatch | Use automation tools to detect and report any unauthorized machines                       | detecting | <p><a href="https://man.archlinux.org/man/arp-scan.1.en">https://man.archlinux.org/man/arp-scan.1.en</a><br><a href="https://man.archlinux.org/man/arpwatch.8.en">https://man.archlinux.org/man/arpwatch.8.en</a></p> |

## Automation

| Tools                | Description                                                                                                                                                                                                                               | Purpose                  | Links                                                                                                                                                          |
| -------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Ansible-Playbooks    | Leverage Ansible for automation of infrastructure deployment. Ensure consistency and reliability through version-controlled playbooks                                                                                                     | automation of deployment | [https://docs.ansible.com/ansible/latest/playbook\_guide/playbooks\_intro.html](https://docs.ansible.com/ansible/latest/playbook\_guide/playbooks\_intro.html) |
| Helm                 | The package manager for Kubernetes. Helm helps you manage Kubernetes applications                                                                                                                                                         | automation of deployment | [https://helm.sh/](https://helm.sh/)                                                                                                                           |
| AWS-Launch Templates | Employ AWS Launch Templates for efficient and standardized instance provisioning. Push templates into a repository and ensure it is version-controlled. Leverage template parameters to customize instances as per specific requirements. | automation of deployment | [https://docs.aws.amazon.com/autoscaling/ec2/userguide/launch-templates.html](https://docs.aws.amazon.com/autoscaling/ec2/userguide/launch-templates.html)     |
| Terraform            | Automate infrastructure on any cloud                                                                                                                                                                                                      | automation of deployment | [https://www.terraform.io/](https://www.terraform.io/)                                                                                                         |

## MFA on Servers

| Tools                           | Description                                  | Purpose            | Links                                                                                                          |
| ------------------------------- | -------------------------------------------- | ------------------ | -------------------------------------------------------------------------------------------------------------- |
| Google Authenticator PAM module | Implement MFA for all administrative access. | secure your server | [https://github.com/google/google-authenticator-libpam](https://github.com/google/google-authenticator-libpam) |
| YubiHSM                         | Hardware-based authentication methods        | secure your server | [https://developers.yubico.com/YubiHSM2/Usage\_Guides/](https://developers.yubico.com/YubiHSM2/Usage\_Guides/) |
| SSH Key rotation                | Use SSH Private Keys Instead of Passwords    | secure your server | [https://docs.aws.amazon.com/secretsmanager/](https://docs.aws.amazon.com/secretsmanager/)                     |

## Key Security

| Tools     | Description                        | Purpose                  | Links                                            |
| --------- | ---------------------------------- | ------------------------ | ------------------------------------------------ |
| Bitwarden | Store keys securely in a key vault | secure your keys, access | [https://bitwarden.com/](https://bitwarden.com/) |

## Firewall

| Tools               | Description                                                                                                       | Purpose         | Links                                                                                                                                                                                                                            |
| ------------------- | ----------------------------------------------------------------------------------------------------------------- | --------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| UFW                 | No direct SSH/RDP should be accessible from the internet.                                                         | protect servers | [https://wiki.archlinux.org/title/Uncomplicated\_Firewall](https://wiki.archlinux.org/title/Uncomplicated\_Firewall)                                                                                                             |
| AWS Security Groups | Control traffic to your AWS resources using security groups. Access should be enabled through an MFA-enabled VPN. | protect servers | [https://docs.aws.amazon.com/vpc/latest/userguide/security-group-rules.html#security-group-rule-characteristics](https://docs.aws.amazon.com/vpc/latest/userguide/security-group-rules.html#security-group-rule-characteristics) |

## IP-based DDoS Mitigation

| Tools                          | Description                                                             | Purpose                                          | Links                                                                                        |
| ------------------------------ | ----------------------------------------------------------------------- | ------------------------------------------------ | -------------------------------------------------------------------------------------------- |
| AWS Shield                     | All AWS customers benefit from the automatic protections of AWS Shield. | DDoS protection                                  | [https://aws.amazon.com/shield/](https://aws.amazon.com/shield/)                             |
| Setup Nodeexporter for Grafana | Setup Grafana Alerts with thresholds for incoming and outgoing Traffic. | Regularly monitor network traffic for anomalies. | [https://github.com/prometheus/node\_exporter](https://github.com/prometheus/node\_exporter) |



## Engine API Being Filtered + Auth for Engine API

<table><thead><tr><th width="124">Tools</th><th>Description</th><th>Purpose</th><th>Links</th></tr></thead><tbody><tr><td>nginx, firewalls + your el/cl-configuration files</td><td>Filter access to the Engine API or disable unnecessary API's in your Beacon/Exection-layer nodes configuration files.*</td><td>prevent api attacks</td><td><a href="https://www.nginx.com/">https://www.nginx.com/</a></td></tr></tbody></table>

\* Note \
By default, account unlocking is forbidden when HTTP or Websocket access is enabled (i.e. by passing --http or ws flag). This is because an attacker that manages to access the node via the externally-exposed HTTP/WS port can then control the unlocked account. It is possible to force account unlock by including the --allow-insecure-unlock flag but this is unsafe and not recommended except for expert users that completely understand how it can be used safely. This is not a hypothetical risk: there are bots that continually scan for http-enabled Ethereum nodes to attack

## VLAN Segmentation

| Tools    | Description                                                                                        | Purpose                                                                                    | Links                                                                                                                                                                                                                                                                      |
| -------- | -------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| mikrotik | Group related servers and services into VLANs. Subnet and connect your network and cloud networks. | Limit inter-VLAN routing to only necessary services with Site to Site IPsec (IKEv2) tunnel | [https://mikrotik.com/download](https://mikrotik.com/download), [https://help.mikrotik.com/docs/display/ROS/IPsec#IPsec-SitetoSiteGREtunneloverIPsec(IKEv2)usingDNS](https://help.mikrotik.com/docs/display/ROS/IPsec#IPsec-SitetoSiteGREtunneloverIPsec\(IKEv2\)usingDNS) |

## OS Hardening

| Tools   | Description                                                                         | Purpose     | Links                                                                                                                                                                        |
| ------- | ----------------------------------------------------------------------------------- | ----------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| SELinux | Use hardening playbooks that automate many of these processes and activate SELinux. | OS security | [https://wiki.archlinux.org/title/Security](https://wiki.archlinux.org/title/Security), [https://wiki.archlinux.org/title/SELinux](https://wiki.archlinux.org/title/SELinux) |

## EDR, SIEM, NDR

| Tools | Description                                                     | Purpose                       | Links                                                            |
| ----- | --------------------------------------------------------------- | ----------------------------- | ---------------------------------------------------------------- |
| EDR   | EDR for endpoint-level visibility                               | secure endpoint               | multiple provider                                                |
| SIEM  | SIEM for comprehensive security event management and reporting. | security events and reporting | [https://github.com/wazuh/wazuh](https://github.com/wazuh/wazuh) |
| NDR   | NDR for network-level monitoring and response.                  | monitor network               | multiple provider                                                |
