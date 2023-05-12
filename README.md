# Cisco Networks Add-on

[![GitHub contributors](https://img.shields.io/github/contributors/inspired/TA-cisco_ios.svg)]()

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
| App Version | 2.7.4 |
| Vendor Products | Cisco Catalyst, ASR, ISR, Nexus, CRS and other IOS based switches, Wireless LAN Controller, ACI |
| Has index-time operations | True |
| Create an index | False |
| Implements summarization | False |

The Cisco Networks Add-on allows a Splunk® Enterprise administrator to extract and filter event information from Cisco IOS and WLC devices. The app sets the correct sourcetype and adds fields required for CIM compliance, and must be installed in order for the Cisco Networks App to work.

##### Scripts and binaries

No scripts or binaries are included.

#### Release notes

##### About this release

Version 2.7.4 of the Cisco Networks Add-on is compatible with:

| Splunk Enterprise/Cloud versions | 9.0+, 8.2, 8.1 |
| --- | --- |
| CIM | 4.* |
| Platforms | Platform independent |
| Vendor Products | Cisco Catalyst, ASR, ISR, Nexus, CRS and other IOS based switches, Wireless LAN Controller, ACI |
| Lookup file changes | Added cisco_ios_aci_fault_codes, Removed cisco_ios_apptype |

##### New features

Cisco Networks Add-on includes the following new features:

- Added extractions for some of the %SESSION_MGR messages
- Added GigabitEthernet,FastEthernet and Ethernet to the interface name lookup
- Added samples of %SESSION_MGR for eventgen

##### Fixed issues

Version 2.7.4 of the Cisco Networks Add-on fixes the following issues:

- None known
##### Known issues

Version 2.7.4 of the Cisco Networks Add-on has the following known issues:

- None known

##### Third-party software attributions

Version 2.7.4 of the Cisco Networks Add-on incorporates the following third-party software or libraries.

- Icon by Yudha Agung Pribadi (https://www.iconfinder.com/iconsets/networking-icons-1)

##### Support and resources

**This app is community supported on a best effort basis. In case you have needs for professional support billed by the hour, please contact the author.

* Access questions and answers specific to the Cisco Networks Add-on at http://answers.splunk.com/app/questions/1467.html

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

- Optional: Cisco Networks App, 2.7.1 or higher (for dashboards etc)

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

This add-on should not be installed on forwarders unless you are monitoring your logs using the Heavy Forwarder. In that case, install this add-on on your Heavy Forwarder in addition to your indexers and search heads

##### Deploy to distributed deployment with Search Head Pooling
Follow the same steps as *Install to search head*.
##### Deploy to distributed deployment with Search Head Clustering
Follow the same steps as *Install to search head*.
##### Deploy to Splunk Cloud
Follow the same steps as *Install to search head*.
#### Configure Cisco Networks Add-on

1. Install in $SPLUNK_HOME/etc/apps/TA-cisco_ios

2. Create a UDP input on one of your Splunk servers or a forwarder with sourcetype set to *syslog* or *cisco:ios*. A regex match will be performed to rewrite the events to the cisco:ios sourcetype.
3. Configure your Cisco devices to send their syslogs to the UDP input created in step 2 with logging level informational.

4. Restart Splunk

## USER GUIDE

### Data types

This app provides search-time knowledge for the following types of data from Cisco IOS variants, NX-OS and WLC:

**Search-time**

- cisco:ios - Syslog events from your devices

These data types support the following Common Information Model data models:

| Source Type | CIM Data Models |
| --- | --- |
| cisco:ios | Change Analysis<br/>Authentication<br/>Network Traffic<br/>|


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

**cisco_ios_icmp_code.csv**

Provides ICMP code lookups for ACL events. Needed for CIM compliance

- File location: lookups/cisco_ios_icmp_code.csv
- Lookup fields: icmp_code_id, icmp_code, reference
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

**cisco_ios_aci_fault_codes.csv**

ACI fault codes

- File location: lookups/cisco_ios_aci_fault_codes.csv
- Lookup fields: fault_code, vendor_explanation, vendor_recommended_action
- Lookup contents: See the file contents
