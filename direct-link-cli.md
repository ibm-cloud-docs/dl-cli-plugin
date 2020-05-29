---

copyright:
  years: 2020
lastupdated: "2020-02-12"

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

# Direct Link 2.0 CLI reference
{: #dl-cli}

This document provides a reference of the command-line interface (CLI) commands available for {{site.data.keyword.cloud}} Direct Link Dedicated. The commands are organized into the sections that are listed in the navigation pane on the right.  
{:shortdesc}

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

## ibmcloud dl gateway
{: #get-help-specific-gateway}

View details of a specific gateway.

```
ibmcloud dl gateway|gw GATEWAY_ID [-–help|-h] [--output format]
```

### Command options
{: #command-options-gateway-view-details}

- **GATEWAY_ID**<br />Specify the ID of the gateway.
- **--help|-h**<br />(Optional) Get help on this command.
- **--output value**<br />Optional: Specify whether you want the output that is displayed in JSON format. Currently, **json** is the only supported format.

### Examples
{: #example-get-gateway}

```
ibmcloud dl gateway a771366f-2c8c-49f6-a23b-9d49fad035a3
```

```
ibmcloud dl gw a771366f-2c8c-49f6-a23b-9d49fad035a3 --output json
```

---

## ibmcloud dl gateways
{: #list-all-gateways}

List all gateways.

```
ibmcloud dl gateways|gws [-–help|-h] [--output format]
```

### Command options
{: #command-options-help-list-gateways}

- **--help|-h**<br />(Optional) Get help on this command.
- **--output value**<br />Optional: Specify whether you want the output that is displayed in JSON format. Currently, **json** is the only supported format.

---

## ibmcloud dl gateway-create
{: #create-gateway}

Create a gateway.

```
ibmcloud dl gateway-create|gwc GATEWAY_NAME --bgp-asn BGP_ASN --cross-connect-router CROSS_CONNECT_ROUTER  --location-name LOCATION_NAME --speed-mbps SPEED_MBPS --type TYPE [--global] [--metered] [--bgp-base-cidr BGP_IP_CIDR] [--bgp-ibm-cidr BGP_IBM_CIDR] [--bgp-cer-cidr BGP_CER_CIDR] [--resource-group-id RESOURCE_GROUP_ID] [--carrier-name CARRIER_NAME] [--customer-name CUSTOMER_NAME] [-–help|-h] [--output format]
```

 ### Command options
{: #command-options-gateway-create}

- **GATEWAY_NAME**<br />Specify a name for the new gateway.
- **--bgp-asn VALUE**<br />Specify either the default value of **64999**, or select an ASN from allowed ranges.
- **--cross-connect-router XCR**<br />Select the IBM cross-connect router for the Direct Link connection.
- **--location-name LOCATION**<br />Specify the location name; for example, **dal10**.
- **--speed-mbps SPEED_MBPS**<br />Specify a value for the speed.
- **--type TYPE**<br />Specify the Direct Link offering type. Currently, only **dedicated** is supported.
- **--global**<br />Enable global routing. Gateways with global routing can connect to network outside their region. Set to **false** by default.
- **--metered**<br />Specify a billing option. Set to **false** by default.
- **--bgp-base-cidr CIDR:**<br />Specify the CIDR.
- **--bgp-ibm-cidr CIDR:**<br />Specify the CIDR.
- **--bgp-cer-cidr CIDR:**<br />Specify the CIDR.
- **--resource-group-id value**<br />Resource group ID for this resource. If unspecified, the account's default resource group is used.
- **--carrier-name value**<br />Specify the gateway CARRIER NAME.
- **--customer-name value**<br />Sprecify the gateway CUSTOMER NAME.
- **--help|-h**<br />(Optional) Get help on this command.
- **--output value**<br />(Optional) Specify whether you want the output that is displayed in JSON format. Currently, **json** is the only supported format.

### Examples
{: #example-create-gateway}

```
ibmcloud dl gateway-create dl-gw --bgp-asn 64999 --cross-connect-router LAB-xcr01.dal09 --global --metered --location-name dal09 --speed-mbps 1000 --type dedicated --bgp-base-cidr 169.254.0.51/30 --bgp-ibm-cidr 169.254.0.52/30 --bgp-cer-cidr 169.254.0.53/30
```

```
ibmcloud dl gateway-create dl-gw --bgp-asn 64999 --cross-connect-router LAB-xcr01.dal09 --global --metered --location-name dal09 --speed-mbps 1000 --type dedicated --bgp-base-cidr 169.254.0.51/30 --bgp-ibm-cidr 169.254.0.52/30 --bgp-cer-cidr 169.254.0.53/30 --output json
```

---

## ibmcloud dl gateway-delete
{: #delete-gateway}

Delete a specific gateway.

```
ibmcloud dl gateway-delete|gwd GATEWAY_ID [--help|-h] [--force|-f]
```

### Command options
{: #command-options-gateway-delete}

- **GATEWAY_ID**<br />Specify the ID of the gateway.
- **--help|-h**<br />(Optional) Get help on this command.   
- **--force|-f**<br />(Optional) Force the delete operation without confirmation.

### Examples
{: #example-delete-gateway1}

```
ibmcloud dl gateway-delete e281b18b-0dba-49ee-9c64-aea588b7f1fd
```

```
ibmcloud dl gateway-delete 8ba9e7b0-dded-400e-ad7e-6481dad0b157 -f
```

---

## ibmcloud dl gateway-update
{: #update-gateway}

Update a specific gateway.

```
ibmcloud dl gateway-update|gwu GATEWAY_ID [--global VALUE] [--speed-mbps SPEED_MBPS] [--loa-reject-reason LOA_REJECT_REASON] [--operational-status OPERATIONAL_STATUS] [--help|-h] [--output format]
```

### Command options
{: #command-options-specific-gateway}

- **GATEWAY_ID**<br />Specify the ID of the gateway.
- **--global VALUE**<br />Gateways with global routing can connect to networks outside their region. Specify a **true** or **false** value.
- **--speed-mbps SPEED_MBPS**<br />Specify the speed of the gateway in MBPS.
- **--loa-reject-reason LOA_REJECT_REASON**<br />Specify the reason for the Letter of Authorization (LOA) rejection.
- **--operational-status OPERATIONAL_STATUS**<br />Specify the gateway's operational status. Values are **loa_accepted** or **loa_rejected**.
- **--help|-h**<br />(Optional) Get help on this command.
- **--output value**<br />(Optional) Specify whether you want the output that is displayed in JSON format. Currently, **json** is the only supported format.

### Examples
{: #example-update-gateway1}

```
ibmcloud dl gateway-update 8ba9e7b0-dded-400e-ad7e-6481dad0b157 --speed-mbps 5000 --name dl-gw-updated
```

```
ibmcloud dl gateway-update 8ba9e7b0-dded-400e-ad7e-6481dad0b157 --speed-mbps 5000 --name dl-gw-updated --output json
```

---

## ibmcloud dl location
{: #location-retrieve}

Retrieves location-specific information for a specific offering type.

```
ibmcloud dl location|loc LOCATION_NAME OFFERING_TYPE [--help|-h] [--output format]
```

### Command options
{: #command-options-location}

- **LOCATION_NAME**<br />Specify the name of the location.
- **OFFERING_TYPE**<br />Specify the Direct Link offering type. Values are **dedicated** or **dedicated_hosting**.
- **--help|-h**<br />(Optional) Get help on this command.
- **--output value**<br />(Optional) Specify whether you want the output that is displayed in JSON format. Currently, **json** is the only supported format.  

### Examples
{: #example-update-location}

```
ibmcloud dl location "Washington 2" dedicated
```

```
ibmcloud dl loc "Washington 2" dedicated --output json
```

---

## ibmcloud dl locations
{: #list-locations-offering-type-json}

List the locations for a specific Direct Link offering type.

```
ibmcloud dl locations|locs OFFERING_TYPE [–-output format] [--help|-h]
```

### Command options
{: #command-options-offering_type}

- **OFFERING_TYPE**<br />Specify the Direct Link offering type. Values are **dedicated** or **dedicated_hosting**.
- **--output value**<br />(Optional) Specify whether you want the output that is displayed in JSON format. Currently, **json** is the only supported format.
- **--help|-h**<br />(Optional) Get help on this command.   

### Examples
{: #example-offering-type1}

```
ibmcloud dl locations dedicated
```

```
ibmcloud dl locs dedicated --output json
```

---

## ibmcloud dl offering-speeds
{: #offering-speeds-list}

Lists all offering speeds for an offering type.

```
ibmcloud dl offering-speeds|ospeeds OFFERING_TYPE [--output format] [--help|-h]
```

### Command options
{: #command-options-offering-speeds-type}

- **OFFERING_TYPE**<br />Specify the Direct Link offering type. Values are **dedicated** or **dedicated_hosting**.
- **--output value**<br />(Optional) Specify whether you want the output that is displayed in JSON format. Currently, **json** is the only supported format.
- **--help|-h**<br />(Optional) Get help on this command.   

### Examples
{: #example-offering-type}

```
ibmcloud dl offering-speeds dedicated
```

```
ibmcloud dl ospeeds dedicated_hosting --output json
```

---

## ibmcloud dl virtual-connections
{: #virtual-connections-list}

List virtual connections.

```
ibmcloud dl virtual-connections|vcs [--help|-h] [--output format]
```

### Command options
{: #command-options-offering-speeds}

- **--help|-h**<br />(Optional) Get help on this command.  
- **--output value**<br />(Optional) Specify whether you want the output that is displayed in JSON format. Currently, **json** is the only supported format.

### Examples
{: #example-list-details-virtual-connection}

```
ibmcloud dl virtual-connections a771366f-2c8c-49f6-a23b-9d49fad035a3
```

```
ibmcloud dl vcs a771366f-2c8c-49f6-a23b-9d49fad035a3 --output json
```

---

## ibmcloud dl virtual-connection
{: #virtual-connection-view}

View details of a virtual connection.

```
ibmcloud dl virtual-connection|vc GATEWAY_ID VIRTUAL_CONNECTION_ID [--output format] [--help|-h]
```

### Command options
{: #command-options-view-details-virtual-connection}

- **GATEWAY_ID**<br />Specify the ID of the gateway.
- **VIRTUAL_CONNECTION_ID**<br />Specify the ID of the virtual connection.
- **--output value**<br />(Optional) Specify whether you want the output that is displayed in JSON format. Currently, **json** is the only supported format.
- **--help|-h**<br />(Optional) Get help on this command.   

### Examples
{: #example-show-details-virtual-connection}

```
ibmcloud dl virtual-connection a771366f-2c8c-49f6-a23b-9d49fad035a3 dea35ba0-7323-4d8d-9c8d-d7ecda55e23d
```

```
ibmcloud dl vc a771366f-2c8c-49f6-a23b-9d49fad035a3 dea35ba0-7323-4d8d-9c8d-d7ecda55e23d --output json
```

---

## ibmcloud dl virtual-connection-create
{: #virtual-connection-create}

Creating a virtual connection.

```
ibmcloud dl virtual-connection-create|vcc --type TYPE --network-id NETWORK_ID --name VIRTUAL_CONNECTION_NAME [--help|-h] [--output format]
```

### Command options
{: #command-options-create-virtual-connection}

- **--type TYPE**<br />Specify the type of virtual connection. Values are **classic** or **vpc**.
- **--network-id NETWORK_ID**<br />Specify the ID of the network. Not required when using **classic** type.
- **--name NAME**<br />Specify the name of the virtual connection.
- **--output value**<br />(Optional) Specify whether you want the output that is displayed in JSON format. Currently, **json** is the only supported format.
- **--help|-h**<br />(Optional) Get help on this command.   

### Examples
{: #example-create-virtual-connection}

```
ibmcloud dl virtual-connection-create fb0df64a-ef8d-4b3c-b473-dc0230593529 --type vpc --network-id crn:v1:staging:public:is:us-south:a/28e4d90ac7504be694471ee66e70d0d5::vpc:r134-b8b62f60-f152-471f-971a-376da52721e0 --name newVC
```

```
ibmcloud dl vcc fb0df64a-ef8d-4b3c-b473-dc0230593529 --type vpc --network-id crn:v1:staging:public:is:us-south:a/28e4d90ac7504be694471ee66e70d0d5::vpc:r134-b8b62f60-f152-471f-971a-376da52721e0 --name newVC --output json
```

---

## ibmcloud dl virtual-connection-delete
{: #delete-virtual-connection}

Delete a virtual connection.

```
ibmcloud dl virtual-connection-delete|vcd GATEWAY_ID VIRTUAL_CONNECTION_ID [--help|-h] [--force|-f]
```

### Command options
{: #command-options-delete-virtual-connection}

- **GATEWAY_ID**<br />Specify the ID of the gateway.
- **VIRTUAL_CONNECTION_ID**<br />Specify the ID of the virtual connection.
- **--help|-h**<br />(Optional) Get help on this command.   
- **--force|-f**<br />(Optional) Force the delete operation without confirmation.

### Examples
{: #example-delete-virtual-connection}

```
ibmcloud dl virtual-connection-delete fb0df64a-ef8d-4b3c-b473-dc0230593529 0b1e165c-a89c-4682-9771-dbe062e3acf7
```

```
ibmcloud dl vcd fb0df64a-ef8d-4b3c-b473-dc0230593529 26284b6e-78a9-416c-ba5e-2b6ec085f18b -f
```

---

## ibmcloud dl virtual-connection-update
{: #example-update-virtual-connection}

Update a virtual connection.

```
ibmcloud dl virtual-connection-update|vcu [--name NAME] [--status STATUS] [--help|-h] [--output format]
```

### Command options
{: #command-options-update-virtual-connection}

- **--name NAME**<br />Specify the name of the virtual connection.
- **--status STATUS**<br />Specify the virtual connection status. Values are **attached** or **rejected**.
- **--help|-h**<br />(Optional) Get help on this command.
- **--output value**<br />(Optional) Specify whether you want the output that is displayed in JSON format. Currently, **json** is the only supported format.

### Examples
{: #example-update-virtual}

```
ibmcloud dl virtual-connection-update fb0df64a-ef8d-4b3c-b473-dc0230593529 3d577350-9450-4fd0-94b6-2f6da21b828e --name newVCUpdated
```

```
ibmcloud dl vcu adaa0879-3509-4e71-b02b-0c7587ccbcfa 9b11fa61-6e74-4a8f-b978-bca1bead097f --name newVCUpdated --output json
```

---

## ibmcloud dl loa
{: #loa-download}

Download the LOA for the specified gateway in either the current, working directory or in the specified directory.

```
ibmcloud dl loa GATEWAY_ID [--file OUTPUT_DIRECTORY_PATH] [--help|-h]
```

### Command options
{: #command-options-loa-download}

- **GATEWAY_ID**<br />Specify the ID of the gateway.
- **--file OUTPUT_DIRECTORY_PATH**<br />(Optional) Specify the output directory path. For example, specify to download the LOA in the **/tmp** directory.
- **--help|-h**<br />(Optional) Get help on this command.   

### Examples
{: #example-loa-download}

```
ibmcloud dl loa 5cc19d0a-792c-4595-adfc-f90fc650de01
```

```
ibmcloud dl loa 5cc19d0a-792c-4595-adfc-f90fc650de01 --file /tmp
```

---

## ibmcloud dl completion-notice
{: #completion-notice-download}

Download the completion notice for the specified gateway in either the current, working directory or in a specified output directory path.

```
ibmcloud dl completion-notice|cn GATEWAY_ID [--file OUTPUT_DIRECTORY_PATH][--help|-h]
```

### Command options
{: #command-options-completion-notice-download}

- **GATEWAY_ID**<br />Specify the ID of the gateway.
- **--file OUTPUT_DIRECTORY_PATH**<br />(Optional) Specify the output directory path where you want to download the completion notice. For example, specify to download the completion notice in the **/tmp** directory.
- **--help|-h**<br />(Optional) Get help on this command.   

### Examples
{: #example-completion-notice-download}

```
ibmcloud dl completion-notice 0e28b9bc-06df-44f1-b5d7-08085b9fc935
```

```
ibmcloud dl cn 0e28b9bc-06df-44f1-b5d7-08085b9fc935 --file /tmp
```

---

## ibmcloud dl completion-notice-update
{: #completion-notice-upload}

Upload the completion notice from either the working directory or a specified directory.

```
ibmcloud dl completion-notice-update GATEWAY_ID [-i INPUT_DIRECTORY_PATH]
```

### Command options
{: #command-options-completion-notice-upload}

- **GATEWAY_ID**<br />Specify the ID of the gateway.
- **-i INPUT_DIRECTORY_PATH**<br />(Optional) Specify the directory in which you want to upload the completion notice.

### Examples
{: #example-completion-notice-upload}

```
ibmcloud dl completion-notice-update 5cc19d0a-792c-4595-adfc-f90fc650de01
```

```
ibmcloud dl cnu 22f799e8-b4ab-44ca-856b-897be9b0e53d -i /tmp/
```
