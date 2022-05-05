[comment]: # "Auto-generated SOAR connector documentation"
# Akamai WAF

Publisher: Robert Drouin  
Connector Version: 1\.1\.0  
Product Vendor: Akamai  
Product Name: Network Lists  
Product Version Supported (regex): "\.\*"  
Minimum Product Version: 5\.2\.0  

The WAF API allows you to manage a common set of lists for use in various Akamai security products such as Kona Site Defender, Web App Protector, and Bot Manager

[comment]: # "File: README.md"
[comment]: # ""
[comment]: # "    Licensed under Apache 2.0 (https://www.apache.org/licenses/LICENSE-2.0.txt)"
[comment]: # ""
The Network Lists API allows you to manage a common set of lists for use in various Akamai security
products such as Kona Site Defender, Web App Protector, and Bot Manager. Network lists are shared
sets of IP addresses, CIDR blocks, or broad geographic areas. Along with managing your own lists,
you can also access read-only lists that Akamai dynamically updates for you.

## Port Information

The app uses HTTP/ HTTPS protocol for communicating with the Akamai WAF server. Below are the
default ports used by Splunk SOAR.

|         Service Name | Transport Protocol | Port |
|----------------------|--------------------|------|
|         http         | tcp                | 80   |
|         https        | tcp                | 443  |


### Configuration Variables
The below configuration variables are required for this Connector to operate.  These variables are specified when configuring a Network Lists asset in SOAR.

VARIABLE | REQUIRED | TYPE | DESCRIPTION
-------- | -------- | ---- | -----------
**base\_url** |  required  | string | Base URL for the API\. This URL is given to you when you setup the API Client in the Akamai Control Center\. e\.g\. https\://akaa\-WWWWWWWWWWWW\.luna\.akamaiapis\.net
**access\_token** |  required  | password | Access Token for the API
**client\_token** |  required  | password | Client Token for the API
**client\_secret** |  required  | password | Client Secret for the API

### Supported Actions  
[test connectivity](#action-test-connectivity) - Validate the asset configuration for connectivity using the supplied configuration  
[list networks](#action-list-networks) - Get a network list  
[get network](#action-get-network) - Gets a network list's most recent syncPoint version  
[create network](#action-create-network) - Create a new network list  
[delete network](#action-delete-network) - Removes a network list  
[update network](#action-update-network) - Update the network list items and properties  
[add element](#action-add-element) - Adds the specified element\(s\) to a list  
[remove element](#action-remove-element) - Remove the specified element\(s\) from the list  
[activate network](#action-activate-network) - Activate the most recent syncPoint version of a network list in either the STAGING or PRODUCTION environment  
[activation status](#action-activation-status) - Shows a network list activation status on either the STAGING or PRODUCTION environment  
[activation snapshot](#action-activation-snapshot) - Gets a version of a network list  
[activation details](#action-activation-details) - Provides detailed status for a given activation  
[list siteshields](#action-list-siteshields) - Get akamai site shields ip ranges  

## action: 'test connectivity'
Validate the asset configuration for connectivity using the supplied configuration

Type: **test**  
Read only: **True**

#### Action Parameters
No parameters are required for this action

#### Action Output
No Output  

## action: 'list networks'
Get a network list

Type: **investigate**  
Read only: **True**

List all network lists available for an authenticated user who belongs to a group, optionally filtered by listType or based on a search string\. For <strong>extended</strong> parameter, when enabled, provides additional response data identifying who and when the lists were created and updated, and the network list's deployment status in both STAGING and PRODUCTION environments\. For <strong>includeelements</strong> parameter, if enabled, the response list includes all items\. For large network lists, this may slow responses and yield large response objects\. Results appear within the networkLists array, which might be empty if no network lists are available to the client\.

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**search** |  optional  | Only list items that match the specified substring in any network list's name or list of items | string | 
**extended** |  optional  | When enabled, provides additional response data \(Default\: false\) | boolean | 
**includeelements** |  optional  | If enabled, the response list includes all items \(Default\: false\) | boolean | 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.parameter\.search | string | 
action\_result\.parameter\.extended | boolean | 
action\_result\.parameter\.includeelements | boolean | 
action\_result\.data\.\*\.networkLists\.\*\.name | string | 
action\_result\.data\.\*\.networkLists\.\*\.networkListType | string | 
action\_result\.data\.\*\.networkLists\.\*\.elementCount | numeric | 
action\_result\.data\.\*\.networkLists\.\*\.list | string |  `ip` 
action\_result\.data\.\*\.networkLists\.\*\.uniqueId | string |  `akamai networklist id` 
action\_result\.data\.\*\.networkLists\.\*\.type | string | 
action\_result\.data\.\*\.networkLists\.\*\.description | string | 
action\_result\.data\.\*\.networkLists\.\*\.createDate | string | 
action\_result\.data\.\*\.networkLists\.\*\.createdBy | string | 
action\_result\.data\.\*\.networkLists\.\*\.updateDate | string | 
action\_result\.data\.\*\.networkLists\.\*\.updateBy | string | 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary | string | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'get network'
Gets a network list's most recent syncPoint version

Type: **investigate**  
Read only: **True**

For <strong>extended</strong> parameter, when enabled, provides additional response data identifying who and when the lists were created and updated, and the network list's deployment status in both STAGING and PRODUCTION environments\. For <strong>includeelements</strong> parameter, if enabled, the response list includes all items\. For large network lists, this may slow responses and yield large response objects\.

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**networklistid** |  required  | Unique identifier for each network list\. Comma\-separated list is allowed | string |  `akamai networklist id` 
**extended** |  optional  | When enabled, provides additional response data \(Default\: false\) | boolean | 
**includeelements** |  optional  | If enabled, the response list includes all items \(Default\: false\) | boolean | 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.parameter\.networklistid | string |  `akamai networklist id` 
action\_result\.parameter\.extended | boolean | 
action\_result\.parameter\.includeelements | boolean | 
action\_result\.data\.\*\.name | string | 
action\_result\.data\.\*\.networkListType | string | 
action\_result\.data\.\*\.elementCount | numeric | 
action\_result\.data\.\*\.list | string |  `ip` 
action\_result\.data\.\*\.uniqueId | string |  `akamai networklist id` 
action\_result\.data\.\*\.type | string | 
action\_result\.data\.\*\.description | string | 
action\_result\.data\.\*\.createDate | string | 
action\_result\.data\.\*\.createdBy | string | 
action\_result\.data\.\*\.updateDate | string | 
action\_result\.data\.\*\.updatedBy | string | 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary | string | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'create network'
Create a new network list

Type: **generic**  
Read only: **False**

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**name** |  required  | Name for the new network list | string | 
**type** |  required  | Type of the new network list | string | 
**description** |  required  | Description of the new network list | string | 
**list** |  required  | IP\(s\) for the new network list\. Comma\-separated list is allowed | string |  `ip` 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.parameter\.name | string | 
action\_result\.parameter\.type | string | 
action\_result\.parameter\.description | string | 
action\_result\.parameter\.list | string |  `ip` 
action\_result\.data\.\*\.name | string | 
action\_result\.data\.\*\.networkListType | string | 
action\_result\.data\.\*\.elementCount | numeric | 
action\_result\.data\.\*\.list | string |  `ip` 
action\_result\.data\.\*\.uniqueId | string |  `akamai networklist id` 
action\_result\.data\.\*\.type | string | 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary | string | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'delete network'
Removes a network list

Type: **generic**  
Read only: **False**

You can only remove network lists that never activated\. To deactivate a list, you can empty its list of elements\.

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**networklistid** |  required  | Unique identifier for the network list | string |  `akamai networklist id` 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.parameter\.networklistid | string |  `akamai networklist id` 
action\_result\.data\.\*\.status | string | 
action\_result\.data\.\*\.uniqueId | string |  `akamai networklist id` 
action\_result\.data\.\*\.syncPoint | numeric |  `akamai networklist syncpoint` 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary | string | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'update network'
Update the network list items and properties

Type: **generic**  
Read only: **False**

Allows you to set the name, description, and set of network list items to the resource\. The current state of the list will be replaced with the properties and items you provide\. The type cannot be changed\.

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**networklistid** |  required  | Unique identifier for each network list | string |  `akamai networklist id` 
**name** |  required  | Update or change the name of the network list | string | 
**description** |  required  | Update or change the description of the network list | string | 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.parameter\.networklistid | string |  `akamai networklist id` 
action\_result\.parameter\.name | string | 
action\_result\.parameter\.description | string | 
action\_result\.data\.\*\.name | string | 
action\_result\.data\.\*\.networkListType | string | 
action\_result\.data\.\*\.elementCount | numeric | 
action\_result\.data\.\*\.list | string |  `ip` 
action\_result\.data\.\*\.uniqueId | string |  `akamai networklist id` 
action\_result\.data\.\*\.type | string | 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary | string | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'add element'
Adds the specified element\(s\) to a list

Type: **generic**  
Read only: **False**

If the network list's type is IP, the value needs to be a URL\-encoded IP address or CIDR block\.

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**networklistid** |  required  | Unique identifier for the network list | string |  `akamai networklist id` 
**elements** |  required  | Element\(s\) to add to the network list\. Comma\-separated list is allowed | string |  `ip` 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.parameter\.networklistid | string |  `akamai networklist id` 
action\_result\.parameter\.elements | string |  `ip` 
action\_result\.data\.\*\.name | string | 
action\_result\.data\.\*\.networkListType | string | 
action\_result\.data\.\*\.elementCount | numeric | 
action\_result\.data\.\*\.list | string |  `ip` 
action\_result\.data\.\*\.uniqueId | string |  `akamai networklist id` 
action\_result\.data\.\*\.type | string | 
action\_result\.data\.\*\.description | string | 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary | string | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'remove element'
Remove the specified element\(s\) from the list

Type: **generic**  
Read only: **False**

If the network list's type is IP, the value needs to be a URL\-encoded IP address or CIDR block\.

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**networklistid** |  required  | Unique identifier for the network list | string |  `akamai networklist id` 
**elements** |  required  | Element\(s\) to be removed from the network list\. Comma\-separated list is allowed | string |  `ip` 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.parameter\.networklistid | string |  `akamai networklist id` 
action\_result\.parameter\.elements | string |  `ip` 
action\_result\.data\.\*\.name | string | 
action\_result\.data\.\*\.networkListType | string | 
action\_result\.data\.\*\.elementCount | numeric | 
action\_result\.data\.\*\.list | string |  `ip` 
action\_result\.data\.\*\.uniqueId | string |  `akamai networklist id` 
action\_result\.data\.\*\.type | string | 
action\_result\.data\.\*\.description | string | 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary | string | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'activate network'
Activate the most recent syncPoint version of a network list in either the STAGING or PRODUCTION environment

Type: **generic**  
Read only: **False**

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**networklistid** |  required  | Unique identifier for the network list | string |  `akamai networklist id` 
**environment** |  required  | Environment to activate the network \(Default\: STAGING\) | string | 
**comments** |  optional  | Comments to add to the network | string | 
**notification** |  optional  | Notification Recipients for the network list\. Comma\-separated list is allowed | string | 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.parameter\.networklistid | string |  `akamai networklist id` 
action\_result\.parameter\.environment | string | 
action\_result\.parameter\.comments | string | 
action\_result\.parameter\.notification | string | 
action\_result\.data\.\*\.activationId | numeric |  `akamai networklist activationid` 
action\_result\.data\.\*\.activationComments | string | 
action\_result\.data\.\*\.activationStatus | string | 
action\_result\.data\.\*\.syncPoint | numeric |  `akamai networklist syncpoint` 
action\_result\.data\.\*\.uniqueId | string |  `akamai networklist id` 
action\_result\.data\.\*\.fast | boolean | 
action\_result\.data\.\*\.dispatchCount | numeric | 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary | string | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'activation status'
Shows a network list activation status on either the STAGING or PRODUCTION environment

Type: **investigate**  
Read only: **True**

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**networklistid** |  required  | Unique identifier for the network list | string |  `akamai networklist id` 
**environment** |  required  | The environment in which the list activation occurs \(Default\: STAGING\) | string | 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.parameter\.networklistid | string |  `akamai networklist id` 
action\_result\.parameter\.environment | string | 
action\_result\.data\.\*\.activationId | numeric |  `akamai networklist activationid` 
action\_result\.data\.\*\.activationComments | string | 
action\_result\.data\.\*\.activationStatus | string | 
action\_result\.data\.\*\.syncPoint | numeric |  `akamai networklist syncpoint` 
action\_result\.data\.\*\.uniqueId | string |  `akamai networklist id` 
action\_result\.data\.\*\.fast | boolean | 
action\_result\.data\.\*\.dispatchCount | numeric | 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary | string | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'activation snapshot'
Gets a version of a network list

Type: **investigate**  
Read only: **True**

Gets a version of a network list in its state when activated, with each version identified by its syncPoint value\. You can only get syncPoint versions that have been activated\. For <strong>extended</strong> parameter, when enabled, provides additional response data identifying who and when the lists were created and updated, and the network list's deployment status in both STAGING and PRODUCTION environments\.

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**networklistid** |  required  | Unique identifier for the network list | string |  `akamai networklist id` 
**syncpoint** |  required  | The network list version for which to retrieve the snapshot | numeric |  `akamai networklist syncpoint` 
**extended** |  optional  | When enabled, provides additional response data \(Default\: false\) | boolean | 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.parameter\.networklistid | string |  `akamai networklist id` 
action\_result\.parameter\.syncpoint | numeric |  `akamai networklist syncpoint` 
action\_result\.parameter\.extended | boolean | 
action\_result\.data\.\*\.name | string | 
action\_result\.data\.\*\.networkListType | string | 
action\_result\.data\.\*\.elementCount | numeric | 
action\_result\.data\.\*\.list | string |  `ip` 
action\_result\.data\.\*\.uniqueId | string |  `akamai networklist id` 
action\_result\.data\.\*\.type | string | 
action\_result\.data\.\*\.syncPoint | numeric |  `akamai networklist syncpoint` 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary | string | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'activation details'
Provides detailed status for a given activation

Type: **investigate**  
Read only: **True**

Provides detailed status for a given activation, including progress on fast activation and other audit information, in addition to information ordinarily available from the "activation status" action\.

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**activationid** |  required  | Unique identifier for the network list | numeric |  `akamai networklist activationid` 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.parameter\.activationid | numeric |  `akamai networklist activationid` 
action\_result\.data\.\*\.activationId | numeric |  `akamai networklist activationid` 
action\_result\.data\.\*\.createDate | string | 
action\_result\.data\.\*\.createdBy | string | 
action\_result\.data\.\*\.environment | string | 
action\_result\.data\.\*\.fast | boolean | 
action\_result\.data\.\*\.networkList\.activationComments | string | 
action\_result\.data\.\*\.networkList\.activationStatus | string | 
action\_result\.data\.\*\.syncPoint | numeric |  `akamai networklist syncpoint` 
action\_result\.data\.\*\.uniqueId | string |  `akamai networklist id` 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary | string | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'list siteshields'
Get akamai site shields ip ranges

Type: **investigate**  
Read only: **True**

#### Action Parameters
No parameters are required for this action

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.status | string | 
action\_result\.data\.\*\.cidr | string | 
action\_result\.message | string | 
action\_result\.summary\.num\_data | string | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric | 