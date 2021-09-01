---

copyright:
  years: 2020, 2021
lastupdated: "2021-08-16"

keywords: command line interface, commands, CLI

subcollection: dl
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:term: .term}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:external: target="_blank" .external}
{:generic: data-hd-programlang="generic"}
{:download: .download}
{:DomainName: data-hd-keyref="DomainName"}

# Command reference
{: #dl-cli}

This document provides a reference of the command-line interface (CLI) commands available for {{site.data.keyword.cloud}} Direct Link. The commands are organized into the sections that are listed in the navigation pane on the right.  
{: shortdesc}

## Before you begin
{: #cli-ref-prereqs}

Complete these steps to use the Direct Link CLI, which is implemented as an {{site.data.keyword.cloud_notm}} CLI plug-in. This plug-in provides you with the means to manage your service instance and its associated resources through a command-line user interface.

1. Install the [{{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-install-ibmcloud-cli){: external}.
1. Install the **dl-cli** plug-in to the {{site.data.keyword.cloud_notm}} CLI.

   To install the plug-in, enter the following command.

   ```
   ibmcloud plugin install dl-cli
   ```
   {: pre}

---

## ibmcloud plugin show dl-cli
{: #show-plugin-info}

Show Direct Link CLI plug-in information.

```
ibmcloud plugin show dl-cli
```
{: pre}

---

## ibmcloud dl --help
{: #command-help}

Get help on Direct Link commands.

```
ibmcloud dl -h|--help
```
{: pre}

---

## ibmcloud dl completion-notice
{: #completion-notice-download}

Download the completion notice for the specified gateway in either the current, working directory or in a specified output directory path.

```
ibmcloud dl completion-notice|cn GATEWAY_ID [--file OUTPUT_DIRECTORY_PATH][--help|-h]
```
{: pre}

### Command options
{: #command-options-completion-notice-download}

- **GATEWAY_ID**<br />Specify the ID of the gateway.
- **--file OUTPUT_DIRECTORY_PATH**<br />(Optional) Specify the output directory path where you want to download the completion notice. For example, specify to download the completion notice in the **/tmp** directory.
- **--help|-h**<br />(Optional) Get help on this command.   

### Examples
{: #example-completion-notice-download}

- `ibmcloud dl completion-notice 0e28b9bc-06df-44f1-b5d7-08085b9fc935`
- `ibmcloud dl cn 0e28b9bc-06df-44f1-b5d7-08085b9fc935 --file /tmp`

---

## ibmcloud dl completion-notice-update
{: #completion-notice-upload}

Upload the completion notice from either the working directory or a specified directory.

```
ibmcloud dl completion-notice-update GATEWAY_ID [-i INPUT_DIRECTORY_PATH]
```
{: pre}

### Command options
{: #command-options-completion-notice-upload}

- **GATEWAY_ID**<br />Specify the ID of the gateway.
- **-i INPUT_DIRECTORY_PATH**<br />(Optional) Specify the directory in which you want to upload the completion notice.

### Examples
{: #example-completion-notice-upload}

- `ibmcloud dl completion-notice-update 5cc19d0a-792c-4595-adfc-f90fc650de01`
- `ibmcloud dl cnu 22f799e8-b4ab-44ca-856b-897be9b0e53d -i /tmp/`

---

## ibmcloud dl connect-gateway-create
{: #create-connect-gateway}

Create a connect gateway.

The BGP_BASE_CIDR parameter is deprecated, please remove this parameter as it will ignored. See BGP_CER_CIDR and BGP_IBM_CIDR to create a gateway using either automatic or explicit IP assignment.
{: deprecated}

```
ibmcloud dl connect-gateway-create {--file JSON_FILE | GATEWAY_NAME --billing BILLING --bgp-asn BGP_ASN --port-id PORT_ID --routing ROUTING --speed-mbps SPEED_MBPS [--bgp-base-cidr BGP_BASE_CIDR] [--bgp-cer-cidr BGP_CER_CIDR] [--bgp-ibm-cidr BGP_IBM_CIDR] [--connection CONNECTION_TYPE] [--resource-group-id RESOURCE_GROUP_ID]} [--output format]
```
{: pre}

### Command options
{: #command-options-connect-gateway-create}

- **GATEWAY_NAME**<br />Specify a name for the new gateway.
- **--billing VALUE**<br />Billing of resources (metered | non-metered). Select metered to charge per gigabyte and non-metered for flat rate.
- **--bgp-asn VALUE**<br />Specify either the default value of **64999**, or select an ASN from allowed ranges.
- **--bgp-base-cidr BGP_BASE_CIDR:**<br />Specify the BGP Base CIDR.
- **--bgp-cer-cidr BGP_CER_CIDR:**<br />Specify the BGP customer edge router CIDR.
- **--bgp-ibm-cidr BGP_IBM_CIDR:**<br />Specify the BGP IBM CIDR.
- **--bgp-cer-cidr CIDR:**<br />Specify the CIDR.
- **--bgp-ibm-cidr CIDR:**<br />Specify the CIDR.
- **--connection value:**<br />Type of network connection that you want to bind to your direct link. One of: **direct**, **transit**.
- **--file value**<br/>JSON file for input data
- **--port-id**<br />Port ID for the Gateway. Required when type is connect.
- **--resource-group-id value**<br />Resource group ID for this resource. If unspecified, the account's default resource group is used.
- **--routing value**<br />Gateway routing of resources (global | local). Select global to connect resources across regions.
- **--speed-mbps SPEED_MBPS**<br />Specify a value for the speed.
- **--help|-h**<br />(Optional) Get help on this command.
- **--output value**<br />(Optional) Specify whether you want the output that is displayed in JSON format. Currently, **json** is the only supported format.

To enable [MD5 authentication for BGP peers](/docs/dl?topic=dl-dl-md5), use the **--file** option to create the gateway as per the [template](/apidocs/direct_link#create-gateway).
{: note}

### Examples
{: #example-create-connect-gateway}

- `ibmcloud dl connect-gateway-create dl-gw --billing metered --bgp-asn 64999 --bgp-base-cidr 169.254.0.51/30 --port-id 2f41cf65-e72a-4522-9526-e156e4ca02b5 --routing local --speed-mbps 1000 --bgp-cer-cidr 169.254.0.53/30 --bgp-ibm-cidr 169.254.0.52/30 --connection direct`
- `ibmcloud dl connect-gateway-create dl-gw --billing metered --bgp-asn 64999 --bgp-base-cidr 169.254.0.51/30 --port-id 2f41cf65-e72a-4522-9526-e156e4ca02b5 --routing local --speed-mbps 1000 --bgp-cer-cidr 169.254.0.53/30 --bgp-ibm-cidr 169.254.0.52/30 --output json`
- `ibmcloud dl connect-gateway-create --file ~/gateway.json`

---

## ibmcloud dl dedicated-gateway-create
{: #create-dedicated-gateway}

Create a dedicated gateway.

The BGP_BASE_CIDR parameter is deprecated, please remove this parameter as it will ignored. See BGP_CER_CIDR and BGP_IBM_CIDR to create a gateway using either automatic or explicit IP assignment.
{: deprecated}

```
ibmcloud dl dedicated-gateway-create {--file JSON_FILE | GATEWAY_NAME --billing BILLING --bgp-asn BGP_ASN --carrier-name CARRIER_NAME --ccr CROSS_CONNECT_ROUTER --customer-name CUSTOMER_NAME --location-name LOCATION_NAME --routing ROUTING --speed-mbps SPEED_MBPS [--bgp-base-cidr BGP_BASE_CIDR] [--bgp-cer-cidr BGP_CER_CIDR] [--bgp-ibm-cidr BGP_IBM_CIDR] [--connection CONNECTION_TYPE] [--resource-group-id RESOURCE_GROUP_ID]} [--output format]
```
{: pre}

### Command options
{: #command-options-dedicated-gateway-create}

- **GATEWAY_NAME**<br />Specify a name for the new gateway.
- **--billing VALUE**<br />Billing of resources (metered | non-metered). Select metered to charge per gigabyte and non-metered for flat rate.
- **--bgp-asn VALUE**<br />Specify either the default value of **64999**, or select an ASN from allowed ranges.
- **--bgp-base-cidr BGP_BASE_CIDR:**<br />Specify the BGP Base CIDR.
- **--bgp-cer-cidr BGP_CER_CIDR:**<br />Specify the BGP customer edge router CIDR.
- **--bgp-ibm-cidr BGP_IBM_CIDR:**<br />Specify the BGP IBM CIDR.
- **--carrier-name value**<br />Specify the gateway CARRIER NAME.
- **--connection value**<br />Type of network connection that you want to bind to your direct link. One of: **direct**, **transit**.
- **--cross-connect-router XCR**<br />Select the IBM cross-connect router for the Direct Link connection.
- **--customer-name value**<br />Specify the gateway CUSTOMER NAME.
- **--file value**<br/>JSON file for input data
- **--location-name LOCATION**<br />Specify the location name; for example, **dal10**.
- **--resource-group-id value**<br />Resource group ID for this resource. If unspecified, the account's default resource group is used.
- **--routing value**<br />Gateway routing of resources (global | local). Select global to connect resources across regions.
- **--speed-mbps SPEED_MBPS**<br />Specify a value for the speed.
- **--help|-h**<br />(Optional) Get help on this command.
- **--output value**<br />(Optional) Specify whether you want the output that is displayed in JSON format. Currently, **json** is the only supported format.

To create a [MACsec-enabled gateway](/docs/allowlist/dl-macsec?topic=dl-macsec-configure-macsec-direct-link), use the **--file** option to create the gateway as per the [template](/apidocs/direct_link#create-gateway).
{: note}

To enable [MD5 authentication for BGP peers](/docs/dl?topic=dl-dl-md5), use the **--file** option to create the gateway as per the [template](/apidocs/direct_link#create-gateway).
{: note}

### Examples
{: #example-create-dedicated-gateway}

- `ibmcloud dl dedicated-gateway-create dl-gw --billing metered --bgp-asn 64999 --bgp-base-cidr 169.254.0.51/30 --carrier-name carrier --ccr LAB-xcr01.dal09 --customer-name customer --location-name dal09 --routing local --speed-mbps 1000 --bgp-ibm-cidr 169.254.0.52/30 --bgp-cer-cidr 169.254.0.53/30 --connection direct`
- `ibmcloud dl dedicated-gateway-create dl-gw --billing metered --bgp-asn 64999 --bgp-base-cidr 169.254.0.51/30 --carrier-name carrier --ccr LAB-xcr01.dal09 --customer-name customer --location-name dal09 --routing local --speed-mbps 1000 --bgp-ibm-cidr 169.254.0.52/30 --bgp-cer-cidr 169.254.0.53/30 --output json`
- `ibmcloud dl dedicated-gateway-create --file ~/gateway.json`

---

## ibmcloud dl gateway
{: #get-help-specific-gateway}

View details of a specific gateway.

```
ibmcloud dl gateway|gw GATEWAY_ID [-–help|-h] [--output format]
```
{: pre}

### Command options
{: #command-options-gateway-view-details}

- **GATEWAY_ID**<br />Specify the ID of the gateway.
- **--help|-h**<br />(Optional) Get help on this command.
- **--output value**<br />Optional: Specify whether you want the output that is displayed in JSON format. Currently, **json** is the only supported format.

### Examples
{: #example-get-gateway}

- `ibmcloud dl gateway a771366f-2c8c-49f6-a23b-9d49fad035a3`
- `ibmcloud dl gw a771366f-2c8c-49f6-a23b-9d49fad035a3 --output json`

---

## ibmcloud dl gateway-change-approve
{: #gateway-change-approve-cmd}

Approve gateway change request.

```
ibmcloud dl gateway-change-approve GATEWAY_ID {--file JSON_FILE | [--action Action] [--billing BILLING] [--connection CONNECTION_TYPE] [--resource-group-id RESOURCE_GROUP_ID] [--routing ROUTING] [--speed-mbps SPEED_MBPS]} [--output format]
```
{: pre}

### Command options
{: #command-options-gateway-change-approval}

- **GATEWAY_ID**<br />Specify the ID of the gateway.
- **--action ACTION**<br />Action request. One of: **gateway-create**, **gateway-delete**, **gateway-attribute-update**.
- **--billing VALUE**<br />Billing (metered | non-metered). Select metered to charge per gigabyte and non-metered for flat rate. Set for gateway-create requests to select the gateway's metered billing option.
- **-connection value**<br />Type of network connection that you want to bind to your direct link. One of: **direct**, **transit**.
- **--file value**<br/>JSON file for input data
- **--resource-group-id VALUE**<br />Resource group ID for this resource. Set for gateway-create requests to select the gateway's resource group.
- **--routing ROUTING**<br />Gateway routing (global | local). Select global to connect resources across regions.Set for gateway-create requests to select the gateway's routing option.
- **--speed-mbps SPEED_MBPS**<br />Speed of the Gateway in mbps
- **--help|-h**<br />(Optional) Get help on this command.
- **--output value**<br />(Optional) Specify whether you want the output that is displayed in JSON format. Currently, **json** is the only supported format.  

To approve the provider-created gateways with [MD5 authentication for BGP peers](/docs/dl?topic=dl-dl-md5), use the **-file** option to approve the gateway as per the [template](/apidocs/direct_link#create-gateway-action).
{: note}

### Examples
{: #example-gateway-change-approve-ex}

- `ibmcloud dl gateway-change-approve a771366f-2c8c-49f6-a23b-9d49fad035a3 --action gateway-create --routing global --billing metered`
- `ibmcloud dl gateway-change-approve a771366f-2c8c-49f6-a23b-9d49fad035a3 --action gateway-create --routing global --billing metered --connection direct --output json`

---

## ibmcloud dl gateway-change-reject
{: #gateway-change-reject}

Reject gateway change request.

```
ibmcloud dl gateway-change-reject|gwcr GATEWAY_ID [--action Action] [--speed-mbps SPEED_MBPS] [--help|-h] [--output format]
```
{: pre}

### Command options
{: #command-options-gateway-change-approve-parms}

- **GATEWAY_ID**<br />Specify the ID of the gateway.
- **--action ACTION**<br />Action request. One of: **gateway-create**, **gateway-delete**, **gateway-attribute-update**.
- **--speed-mbps SPEED_MBPS**<br />Speed of the Gateway in mbps
- **--help|-h**<br />(Optional) Get help on this command.
- **--output value**<br />(Optional) Specify whether you want the output that is displayed in JSON format. Currently, **json** is the only supported format.  

### Examples
{: #example-gateway-change-reject}

- `ibmcloud dl gateway-change-reject a771366f-2c8c-49f6-a23b-9d49fad035a3 --action gateway-create`
- `ibmcloud dl gateway-change-reject a771366f-2c8c-49f6-a23b-9d49fad035a3 --action gateway-create --output json`

---

## ibmcloud dl gateway-create
{: #create-gateway}

Create a gateway.

This command is deprecated. See [create-connect-gateway](/docs/dl?topic=dl-cli-plugin-dl-cli#create-connect-gateway) and [create-dedicated-gateway](/docs/dl?topic=dl-cli-plugin-dl-cli#create-dedicated-gateway) for creating connect and dedicated gateways respectively.
{: deprecated}

The BGP_BASE_CIDR parameter is deprecated, please remove this parameter as it will ignored. See BGP_CER_CIDR and BGP_IBM_CIDR to create a gateway using either automatic or explicit IP assignment.
{: deprecated}


```
ibmcloud dl gateway-create|gwc GATEWAY_NAME --billing BILLING --bgp-asn BGP_ASN  --bgp-base-cidr BGP_BASE_CIDR --routing ROUTING --speed-mbps SPEED_MBPS --type TYPE [--bgp-cer-cidr BGP_CER_CIDR] [--bgp-ibm-cidr BGP_IBM_CIDR] [--carrier-name CARRIER_NAME] [--cross-connect-router CROSS_CONNECT_ROUTER] [--customer-name CUSTOMER_NAME] [--location-name LOCATION_NAME] [--port-id PORT_ID] [--resource-group-id RESOURCE_GROUP_ID] [-–help|-h] [--output format]
```
{: pre}

### Command options
{: #command-options-gateway-create}

- **GATEWAY_NAME**<br />Specify a name for the new gateway.
- **--billing VALUE**<br />Billing of resources (metered | non-metered). Select metered to charge per gigabyte and non-metered for flat rate.
- **--bgp-asn VALUE**<br />Specify either the default value of **64999**, or select an ASN from allowed ranges.
- **--bgp-base-cidr BGP_BASE_CIDR:**<br />Specify the BGP Base CIDR.
- **--bgp-cer-cidr BGP_CER_CIDR:**<br />Specify the BGP customer edge router CIDR.
- **--bgp-ibm-cidr BGP_IBM_CIDR:**<br />Specify the BGP IBM CIDR.
- **--carrier-name value**<br />Specify the gateway carrier name.
- **--cross-connect-router XCR**<br />Select the IBM cross-connect router for the Direct Link connection.
- **--customer-name value**<br />Specify the gateway customer name.
- **--location-name LOCATION**<br />Specify the location name; for example, **dal10**.
- **--port-id**<br />Port ID for the gateway. Required when type is `connect`.
- **--resource-group-id value**<br />Resource group ID for this resource. If unspecified, the account's default resource group is used.
- **--routing value**<br />Gateway routing of resources (`global | local`). Select global to connect resources across regions.
- **--speed-mbps SPEED_MBPS**<br />Specify a value for the speed.
- **--type TYPE**<br />Specify the Direct Link offering type. One of: **dedicated**, **connect**.
- **--help|-h**<br />(Optional) Get help on this command.
- **--output value**<br />(Optional) Specify whether you want the output that is displayed in JSON format. Currently, **json** is the only supported format.

### Examples
{: #example-create-gateway}

- `ibmcloud dl gateway-create dl-gw --bgp-asn 64999 --cross-connect-router LAB-xcr01.dal09 --routing local --billing metered --location-name dal09 --speed-mbps 1000 --type dedicated --bgp-base-cidr 169.254.0.51/30 --bgp-ibm-cidr 169.254.0.52/30 --bgp-cer-cidr 169.254.0.53/30`
- `ibmcloud dl gateway-create dl-gw --bgp-asn 64999 --cross-connect-router LAB-xcr01.dal09 --routing local --billing metered --location-name dal09 --speed-mbps 1000 --type dedicated --bgp-base-cidr 169.254.0.51/30 --bgp-ibm-cidr 169.254.0.52/30 --bgp-cer-cidr 169.254.0.53/30 --output json`

---

## ibmcloud dl gateway-delete
{: #delete-gateway}

Delete a specific gateway.

```
ibmcloud dl gateway-delete|gwd GATEWAY_ID [--help|-h] [--force|-f]
```
{: pre}

### Command options
{: #command-options-gateway-delete}

- **GATEWAY_ID**<br />Specify the ID of the gateway.
- **--help|-h**<br />(Optional) Get help on this command.   
- **--force|-f**<br />(Optional) Force the delete operation without confirmation.

### Examples
{: #example-delete-gateway1}

- `ibmcloud dl gateway-delete e281b18b-0dba-49ee-9c64-aea588b7f1fd`
- `ibmcloud dl gateway-delete 8ba9e7b0-dded-400e-ad7e-6481dad0b157 -f`

---

## ibmcloud dl gateway-statistics
{: #gateway-statistics}

Fetch the stastics for a specific gateway.

```
ibmcloud dl gateway-statistics|gw-stats GATEWAY_ID --type STATISTIC_TYPE [--help|-h]
```
{: pre}

### Command options
{: #command-options-gateway-statistics}

- **GATEWAY_ID**<br />Specify the ID of the gateway.
- **type value**<br /> Type of the statistics to retrieve. One of: **macsec_mka_session**, **macsec_mka_policy**.
- **--help|-h**<br />(Optional) Get help on this command.

### Example
{: #example-gateway1-statistics}

`ibmcloud dl gateway-statistics e281b18b-0dba-49ee-9c64-aea588b7f1fd --type macsec_mka_session`

---

## ibmcloud dl gateway-update
{: #update-gateway}

Update a specific gateway.

```
ibmcloud dl gateway-update GATEWAY_ID {--file JSON_FILE | [--billing BILLING] [--connection CONNECTION_TYPE] [--loa-reject-reason LOA_REJECT_REASON] [--name NAME] [--operational-status OPERATION_STATUS] [--routing ROUTING] [--speed-mbps SPEED_MBPS]} [--output format]
```
{: pre}

### Command options
{: #command-options-specific-gateway}

- **GATEWAY_ID**<br />Specify the ID of the gateway.
- **--connection value<br />Type of network connection that you want to bind to your direct link. One of: **dedicated**, **connect**.
- **--file value**<br/>JSON file for input data
- **--loa-reject-reason LOA_REJECT_REASON**<br />Specify the reason for the Letter of Authorization (LOA) rejection.
- **--name NAME**<br />Name of the Gateway.
- **--operational-status OPERATIONAL_STATUS**<br />Specify the gateway's operational status. Values are **loa_accepted** or **loa_rejected**.
- **--speed-mbps SPEED_MBPS**<br />Specify the speed of the gateway in MBPS.
- **--routing VALUE**<br />Gateway routing of resources (global | local). Select global to connect resources across regions.
- **--help|-h**<br />(Optional) Get help on this command.
- **--output value**<br />(Optional) Specify whether you want the output that is displayed in JSON format. Currently, **json** is the only supported format.

To clear/update the [MD5 authentication for BGP peers](/docs/dl?topic=dl-dl-md5), use the **--file** option to update the gateway as per the [template](/apidocs/direct_link#update-gateway).
{: note}

### Examples
{: #example-update-gateway1}

- `ibmcloud dl gateway-update 8ba9e7b0-dded-400e-ad7e-6481dad0b157 --speed-mbps 5000 --name dl-gw-updated`
- `ibmcloud dl gateway-update 8ba9e7b0-dded-400e-ad7e-6481dad0b157 --speed-mbps 5000 --name dl-gw-updated --output json`
- `ibmcloud dl gateway-update 8ba9e7b0-dded-400e-ad7e-6481dad0b157 --connection transit --output json`
- `ibmcloud dl gateway-update 8ba9e7b0-dded-400e-ad7e-6481dad0b157 --file ~/gateway-update.json`

---

## ibmcloud dl gateways
{: #list-all-gateways}

List all gateways.

```
ibmcloud dl gateways|gws [-–help|-h] [--output format]
```
{: pre}

### Command options
{: #command-options-help-list-gateways}

- **--help|-h**<br />(Optional) Get help on this command.
- **--output value**<br />Optional: Specify whether you want the output that is displayed in JSON format. Currently, **json** is the only supported format.

---

## ibmcloud dl loa
{: #loa-download}

Download the LOA for the specified gateway in either the current, working directory or in the specified directory.

```
ibmcloud dl loa GATEWAY_ID [--file OUTPUT_DIRECTORY_PATH] [--help|-h]
```
{: pre}

### Command options
{: #command-options-loa-download}

- **GATEWAY_ID**<br />Specify the ID of the gateway.
- **--file OUTPUT_DIRECTORY_PATH**<br />(Optional) Specify the output directory path. For example, specify to download the LOA in the **/tmp** directory.
- **--help|-h**<br />(Optional) Get help on this command.   

### Examples
{: #example-loa-download}

- `ibmcloud dl loa 5cc19d0a-792c-4595-adfc-f90fc650de01`
- `ibmcloud dl loa 5cc19d0a-792c-4595-adfc-f90fc650de01 --file /tmp`

---

## ibmcloud dl location
{: #location-retrieve}

Retrieves location-specific information for a specific offering type.

```
ibmcloud dl location|loc LOCATION_NAME OFFERING_TYPE [--help|-h] [--output format]
```
{: pre}

### Command options
{: #command-options-location}

- **LOCATION_NAME**<br />Specify the name of the location.
- **OFFERING_TYPE**<br />Specify the Direct Link offering type. Currently only **dedicated** is supported.
- **--help|-h**<br />(Optional) Get help on this command.
- **--output value**<br />(Optional) Specify whether you want the output that is displayed in JSON format. Currently, **json** is the only supported format.  

### Examples
{: #example-update-location}

- `ibmcloud dl location "Washington 2" dedicated`
- `ibmcloud dl loc "Washington 2" dedicated --output json`

---

## ibmcloud dl locations
{: #list-locations-offering-type-json}

List the locations for a specific Direct Link offering type.

```
ibmcloud dl locations|locs OFFERING_TYPE [–-output format] [--help|-h]
```
{: pre}

### Command options
{: #command-options-offering_type}

- **OFFERING_TYPE**<br />Specify the Direct Link offering type. Values are **dedicated** or **connect**.
- **--output value**<br />(Optional) Specify whether you want the output that is displayed in JSON format. Currently, **json** is the only supported format.
- **--help|-h**<br />(Optional) Get help on this command.   

### Examples
{: #example-offering-type1}

- `ibmcloud dl locations dedicated`
- `ibmcloud dl locs dedicated --output json`

---

## ibmcloud dl offering-speeds
{: #offering-speeds-list}

Lists all offering speeds for an offering type.

```
ibmcloud dl offering-speeds|ospeeds OFFERING_TYPE [--output format] [--help|-h]
```
{: pre}

### Command options
{: #command-options-offering-speeds-type}

- **OFFERING_TYPE**<br />Specify the Direct Link offering type. Values are **dedicated** or **dedicated_hosting**.
- **--output value**<br />(Optional) Specify whether you want the output that is displayed in JSON format. Currently, **json** is the only supported format.
- **--help|-h**<br />(Optional) Get help on this command.   

### Examples
{: #example-offering-type}

- `ibmcloud dl offering-speeds dedicated`
- `ibmcloud dl ospeeds dedicated_hosting --output json`

---

## ibmcloud dl port
{: #port-retrieve}

View details of a port.

```
ibmcloud dl port PORT_ID [--help|-h] [--output format]
```
{: pre}

### Command options
{: #command-options-port}

- **PORT_ID**<br />Specify the ID of the port.
- **--help|-h**<br />(Optional) Get help on this command.
- **--output value**<br />(Optional) Specify whether you want the output that is displayed in JSON format. Currently, **json** is the only supported format.  

### Examples
{: #example-get-port}

- `ibmcloud dl port a771366f-2c8c-49f6-a23b-9d49fad035a3`
- `ibmcloud dl port a771366f-2c8c-49f6-a23b-9d49fad035a3 --output json`

---

## ibmcloud dl ports
{: #list-all-ports}

List all ports.

```
ibmcloud dl ports [--help|-h] [--output format]
```
{: pre}

### Command options
{: #command-options-ports}

- **--help|-h**<br />(Optional) Get help on this command.
- **--output value**<br />(Optional) Specify whether you want the output that is displayed in JSON format. Currently, **json** is the only supported format.  

### Examples
{: #example-list-ports}

- `ibmcloud dl ports`
- `ibmcloud dl ports --output json`

---

## ibmcloud dl virtual-connection
{: #virtual-connection-view}

View details of a virtual connection.

```
ibmcloud dl virtual-connection|vc GATEWAY_ID VIRTUAL_CONNECTION_ID [--output format] [--help|-h]
```
{: pre}

### Command options
{: #command-options-view-details-virtual-connection}

- **GATEWAY_ID**<br />Specify the ID of the gateway.
- **VIRTUAL_CONNECTION_ID**<br />Specify the ID of the virtual connection.
- **--output value**<br />(Optional) Specify whether you want the output that is displayed in JSON format. Currently, **json** is the only supported format.
- **--help|-h**<br />(Optional) Get help on this command.   

### Examples
{: #example-show-details-virtual-connection}

- `ibmcloud dl virtual-connection a771366f-2c8c-49f6-a23b-9d49fad035a3 dea35ba0-7323-4d8d-9c8d-d7ecda55e23d`
- `ibmcloud dl vc a771366f-2c8c-49f6-a23b-9d49fad035a3 dea35ba0-7323-4d8d-9c8d-d7ecda55e23d --output json`

---

## ibmcloud dl virtual-connection-create
{: #virtual-connection-create}

Creating a virtual connection.

```
ibmcloud dl virtual-connection-create|vcc --type TYPE --network-id NETWORK_ID --name VIRTUAL_CONNECTION_NAME [--help|-h] [--output format]
```
{: pre}

### Command options
{: #command-options-create-virtual-connection}

- **--type TYPE**<br />Specify the type of virtual connection. Values are **classic** or **vpc**.
- **--network-id NETWORK_ID**<br />Specify the ID of the network. Not required when using **classic** type.
- **--name NAME**<br />Specify the name of the virtual connection.
- **--output value**<br />(Optional) Specify whether you want the output that is displayed in JSON format. Currently, **json** is the only supported format.
- **--help|-h**<br />(Optional) Get help on this command.   

### Examples
{: #example-create-virtual-connection}

- `ibmcloud dl virtual-connection-create fb0df64a-ef8d-4b3c-b473-dc0230593529 --type vpc --network-id crn:v1:staging:public:is:us-south:a/28e4d90ac7504be694471ee66e70d0d5::vpc:r134-b8b62f60-f152-471f-971a-376da52721e0 --name newVC`
- `ibmcloud dl vcc fb0df64a-ef8d-4b3c-b473-dc0230593529 --type vpc --network-id crn:v1:staging:public:is:us-south:a/28e4d90ac7504be694471ee66e70d0d5::vpc:r134-b8b62f60-f152-471f-971a-376da52721e0 --name newVC --output json`

---

## ibmcloud dl virtual-connection-delete
{: #delete-virtual-connection}

Delete a virtual connection.

```
ibmcloud dl virtual-connection-delete|vcd GATEWAY_ID VIRTUAL_CONNECTION_ID [--help|-h] [--force|-f]
```
{: pre}

### Command options
{: #command-options-delete-virtual-connection}

- **GATEWAY_ID**<br />Specify the ID of the gateway.
- **VIRTUAL_CONNECTION_ID**<br />Specify the ID of the virtual connection.
- **--help|-h**<br />(Optional) Get help on this command.   
- **--force|-f**<br />(Optional) Force the delete operation without confirmation.

### Examples
{: #example-delete-virtual-connection}
- `ibmcloud dl virtual-connection-delete fb0df64a-ef8d-4b3c-b473-dc0230593529 0b1e165c-a89c-4682-9771-dbe062e3acf7`
- `ibmcloud dl vcd fb0df64a-ef8d-4b3c-b473-dc0230593529 26284b6e-78a9-416c-ba5e-2b6ec085f18b -f`

---

## ibmcloud dl virtual-connection-update
{: #example-update-virtual-connection}

Update a virtual connection.

```
ibmcloud dl virtual-connection-update|vcu [--name NAME] [--status STATUS] [--help|-h] [--output format]
```
{: pre}

### Command options
{: #command-options-update-virtual-connection}

- **--name NAME**<br />Specify the name of the virtual connection.
- **--status STATUS**<br />Specify the virtual connection status. Values are **attached** or **rejected**.
- **--help|-h**<br />(Optional) Get help on this command.
- **--output value**<br />(Optional) Specify whether you want the output that is displayed in JSON format. Currently, **json** is the only supported format.

### Examples
{: #example-update-virtual}

- `ibmcloud dl virtual-connection-update fb0df64a-ef8d-4b3c-b473-dc0230593529 3d577350-9450-4fd0-94b6-2f6da21b828e --name newVCUpdated`
- `ibmcloud dl vcu adaa0879-3509-4e71-b02b-0c7587ccbcfa 9b11fa61-6e74-4a8f-b978-bca1bead097f --name newVCUpdated --output json`

---

## ibmcloud dl virtual-connections
{: #virtual-connections-list}

List virtual connections.

```
ibmcloud dl virtual-connections|vcs [--help|-h] [--output format]
```
{: pre}

### Command options
{: #command-options-offering-speeds}

- **--help|-h**<br />(Optional) Get help on this command.  
- **--output value**<br />(Optional) Specify whether you want the output that is displayed in JSON format. Currently, **json** is the only supported format.

### Examples
{: #example-list-details-virtual-connection}

- `ibmcloud dl virtual-connections a771366f-2c8c-49f6-a23b-9d49fad035a3`
- `ibmcloud dl vcs a771366f-2c8c-49f6-a23b-9d49fad035a3 --output json`
