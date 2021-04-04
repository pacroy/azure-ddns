# azure-ddns

[![Lint Code Base](https://github.com/pacroy/azure-ddns/actions/workflows/linter.yml/badge.svg)](https://github.com/pacroy/azure-ddns/actions/workflows/linter.yml)

Helm Chart to update Azure DNS records to mimic Dynamic DNS service.

## Usage

### Install from Source

Clone this repository to local and execute these commands:

```sh
helm upgrade --install <RELEASE_NAME> . \
    --set clientId="xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx" \
    --set clientSecret="your-client-secret" \
    --set tenantId="xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx" \
    --set resourceGroup="rg-mygroup" \
    --set dnsZone="mydomain.com" \
    --set recordNames="record1 record2" \
    --set updateIpCommand="dig +short myotherdomain.com"
```

### Install from Repository

```sh
helm repo add pacroy https://pacroy.github.io/helm-repo/
helm repo update
helm upgrade --install <RELEASE_NAME> pacroy/azure-ddns \
    --set clientId="xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx" \
    --set clientSecret="your-client-secret" \
    --set tenantId="xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx" \
    --set resourceGroup="rg-mygroup" \
    --set dnsZone="mydomain.com" \
    --set recordNames="record1 record2" \
    --set updateIpCommand="dig +short myotherdomain.com"
```

## Parameters

| Parameter | Description |
| --- | --- |
| schedule | Schedule to run update in Cron expression. Omit to use default of every 5 minutes (`*/5 * * * *`) |
| clientId | AzureAD application ID or ID URI of the [service principal](#Service-Principal) |
| clientSecret | Secret of service principal |
| tenantId | AzureAD tenant ID |
| resourceGroup | Resource group of the DNS zone |
| dnsZone | DNS zone name |
| recordNames | DNS record names, separated by space |
| updateIpCommand | Command to get the up-to-date IP<br />Leave blank use default `curl -fsSL ipv4.icanhazip.com` to use the external IP of the host<br />Or set `dig +short myotherdomain.com` to clone IP from the other domain.  |

