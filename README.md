# Cisco Networks Add-on
## Table of Contents

### OVERVIEW

- About the Cisco Networks Add-on
- Release notes
- Support and resources

### INSTALLATION AND CONFIGURATION

- Hardware and software requirements
- Installation steps
- Deploy to single server instance
- Deploy to distributed deployment
- Deploy to distributed deployment with Search Head Pooling
- Deploy to distributed deployment with Search Head Clustering
- Deploy to Splunk Cloud 
- Configure Cisco Networks Add-on

### USER GUIDE

- Data types
- Lookups

### OVERVIEW

#### About the Cisco Networks Add-on

| Author | Mikael Bjerkeland |
| --- | --- |
| App Version | 2.2.2 |
| Vendor Products | Cisco Catalyst, ASR, ISR, Nexus, CRS and other IOS based switches, Wireless LAN Controller |
| Has index-time operations | True |
| Create an index | False |
| Implements summarization | False |

The Cisco Networks Add-on allows a Splunk® Enterprise administrator to extract and filter event information from Cisco IOS and WLC devices. The app sets the correct sourcetype and adds fields required for CIM compliance, and must be installed in order for the Cisco Networks App to work.

##### Scripts and binaries

No scripts or binaries are included.

#### Release notes

##### About this release

Version 2.2.2 of the Cisco Networks Add-on is compatible with:

| Splunk Enterprise versions | 5.0.x, 6.x |
| --- | --- |
| CIM | 4.2, 4.1, 4.0 |
| Platforms | Platform independent |
| Vendor Products | Cisco Catalyst, ASR, ISR, Nexus, CRS and other IOS based switches, Wireless LAN Controller |
| Lookup file changes | None |

##### New features

Cisco Networks Add-on includes the following new features:

- Direct AP logging now supported. product field can now hold a value of IOS, WLC or IOS
- IP version agnostic IP extractions


##### Fixed issues

Version 2.2.2 of the Cisco Networks Add-on fixes the following issues:

- Transform corrected in case of missing reported_hostname. General field extraction also edited.
- EVAL searchmatch action lookup not working correctly due to conflict with vendor_action lookup. Will need to be fixed by moving all the searchmatches to vendor_action_lookup
- Field extractions for Nexus interface admin changes + tags
- Normalization of src_int in case it contains whitespaces, i.e. "vlan 3333" is now "vlan3333"

##### Known issues

Version 2.2.2 of the Cisco Networks Add-on has the following known issues:

- None known

##### Third-party software attributions

Version 2.2.2 of the Cisco Networks Add-on incorporates the following third-party software or libraries.

- None

##### Support and resources

**Questions and answers**

Access questions and answers specific to the Cisco Networks Add-on at http://answers.splunk.com/app/questions/1467.html.

**Support**

- Consult Splunk Answers tagging your question with Cisco Networks
- Contact the author: mikael@bjerkeland.com


## INSTALLATION AND CONFIGURATION

### Hardware and software requirements

#### Hardware requirements

Cisco Networks Add-On supports the following server platforms in the versions supported by Splunk Enterprise:

- Windows 7, 8, and 8.1 (64-bit)
- Windows Server 2008, 2008 R2, 2012 and 2012 R2 (64-bit)
- Windows 7, and 8 and 8.1 (32-bit)
- Windows Server 2008 (32-bit)
- 2.6+ kernel Linux distributions (64-bit)
- 2.6+ kernel Linux distributions (32-bit)
- Solaris 10, 11 (64-bit)
- Solaris 10, 11 (SPARC)
- OSX 10.8 (Intel)
- OSX 10.9 (Intel)
- OSX 10.10 (Intel)
- FreeBSD 8, and 9 (64-bit)
- AIX 6.1, 7.1

#### Software requirements

To function properly, Cisco Networks Add-on requires the following software:

- Optional: Cisco Networks App, 2.2.0 or higher (for dashboards etc)

#### Splunk Enterprise system requirements

Because this add-on runs on Splunk Enterprise, all of the [Splunk Enterprise system requirements](http://docs.splunk.com/Documentation/Splunk/latest/Installation/Systemrequirements) apply.

#### Download

Download the Cisco Networks Add-on at https://apps.splunk.com/app/1467/.

#### Installation steps

To install and configure this app on your supported platform, follow these steps:

1. In your Splunk Enterprise web interface, click on App(s) -> Manage Apps
1. Click on Install app from file
1. Select the file you downloaded, Click Upload, optionally selecting Upgrade app if you are upgrading from an earlier version. Restart Splunk if required

##### Deploy to single server instance

Follow these steps to install the app in a single server instance of Splunk Enterprise:

1. In your Splunk Enterprise web interface, click on App(s) -> Manage Apps
1. Click on Install app from file
1. Select the file you downloaded, Click Upload, optionally selecting Upgrade app if you are upgrading from an earlier version. Restart Splunk if required

##### Deploy to distributed deployment

**Install to search head**

1. In your Splunk Enterprise web interface, click on App(s) -> Manage Apps
1. Click on Install app from file
1. Select the file you downloaded, Click Upload, optionally selecting Upgrade app if you are upgrading from an earlier version. Restart Splunk if required

**Install to indexers**

1. In your Splunk Enterprise web interface, click on App(s) -> Manage Apps
1. Click on Install app from file
1. Select the file you downloaded, Click Upload, optionally selecting Upgrade app if you are upgrading from an earlier version. Restart Splunk if required

**Install to forwarders**

This app should not be installed on forwarders.

##### Deploy to distributed deployment with Search Head Pooling
Follow the same steps as *Install to search head*.
##### Deploy to distributed deployment with Search Head Clustering
Follow the same steps as *Install to search head*.
##### Deploy to Splunk Cloud
Unknown
#### Configure Cisco Networks Add-on

1. Install in $SPLUNK_HOME/etc/apps/TA-cisco_ios

1. Create a UDP input on one of your Splunk servers or a forwarder with sourcetype set to *syslog* or *cisco:ios*. A regex match will be performed to rewrite the events to the cisco:ios sourcetype.
2. Configure your Cisco devices to send their syslogs to the UDP input created in step 2 with logging level informational.

1. Step 4 to 6: OPTIONAL for Smart Call Home support

1. OPTIONAL - Add a new TCP data input on a port of your choice, set sourcetype to Cisco:SmartCallHome

1. OPTIONAL - On your Cisco devices:

        service call-home
        call-home
        contact-email-addr YOUR.EMAIL@ADDR.ESS
        site-id "YOUR_SITE_NAME"
        profile "Splunk"
        destination transport-method http
        destination address http http://SPLUNK.SERVER.IP:TCP_PORT_FROM_STEP_4
        subscribe-to-alert-group diagnostic severity debug
        subscribe-to-alert-group environment severity debug
        subscribe-to-alert-group inventory
        subscribe-to-alert-group inventory periodic daily 22:30

4. Restart Splunk

## USER GUIDE

### Data types

This app provides search-time knowledge for the following types of data from Cisco IOS variants, NX-OS and WLC:

**Search-time**

- cisco:ios - Syslog events from your devices
- Cisco:SmartCallHome - Inventory data from your devices

These data types support the following Common Information Model data models:

| Source Type | CIM Data Models |
| --- | --- |
| cisco:ios | Change Analysis<br/>Authentication<br/>Network Traffic<br/>|
| Cisco:SmartCallHome | Inventory|


### Lookups

The Cisco Networks Add-on contains 6 lookup files.

**cisco_ios_acl_excluded_ips.csv**

Provides a way to filter local IP addresses from ACL logs.

- File location: lookups/cisco_ios_acl_excluded_ips.csv
- Lookup fields: src_ip
- Lookup contents: See the file contents

**cisco_ios_actions.csv**

Maps a vendor action to a CIM compliant action.

- File location: lookups/cisco_ios_actions.csv
- Lookup fields: vendor_action, action
- Lookup contents: See the file contents

**cisco_ios_apptype.csv**

Provides an app field for CIM compliance.

- File location: lookups/cisco_ios_apptype.csv
- Lookup fields: sourcetype, app
- Lookup contents: See the file contents

**cisco_ios_interface_name.csv**

Normalizes interface names in case an event includes the short form interface name, i.e. Gi0/2 instead of GigabitEthernet0/2.

- File location: lookups/cisco_ios_interface_name.csv
- Lookup fields: int_prefix, int_prefix_long
- Lookup contents: See the file contents

**cisco_ios_severity.csv**

Maps a Cisco severity level to a Splunk compatible CIM severity level as well as mapping severity number identifiers to textual identifiers including descriptions.

- File location: lookups/cisco_ios_severity.csv
- Lookup fields: severity_id, severity, severity_name, severity_id_and_name, severity_description
- Lookup contents: See the file contents

**cisco_ios_vendor.csv**

Provides a vendor field for CIM compliance.

- File location: lookups/cisco_ios_vendor.csv
- Lookup fields: sourcetype, vendor, product
- Lookup contents: See the file contents
