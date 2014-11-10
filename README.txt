Copyright (C) 2013 Mikael Bjerkeland. All Rights Reserved.

App:                    Cisco IOS Technology Add-On
Current Version:        2.1.0
Last Modified:          2014-11-10
Splunk Version:         5.0.x, 6.x
Author:                 Mikael Bjerkeland

The Cisco IOS Technology Add-On (TA) sets the correct sourcetype and fields used for identifying data from Cisco IOS, IOS XE, IOS XR, NX-OS devices

Install this TA on your search head and indexers/heavy forwarders. Install the "Cisco IOS" app on your search head.

Supported data inputs:
*  Syslog  
*  Smart Call Home (HTTP XML)

Please contact me on Splunk Base if there is anything you would like to see in this app.


++ What's New

+++ 2.1.0 (2014-10-11)
Features:
* RFC5424 support (untested). Rewrites sourcetype rfc5424_syslog to cisco:ios if it matches. Also extracts fields

+++ 2.0.0 (2014-09-19)
Features:
* CIM compliance

+++ 1.6.1 (2014-08-21)
Bug fixes:
* IPNAT extraction fixed. Thanks Emmaus Smith!

+++ 1.6.0 (2014-07-21)
Features:
* Lots of new extractions
* Nexus ACL extractions
* IOS Firewall extracts. Thanks Patrick Preuss!
* Cisco IOS XE extraction fix for 4451. Thanks

Bug fixes:
* Cisco IOS Messages CSV file moved from this app to the Cisco IOS app.

+++ 1.5.2 (2014-05-19)
Features:
* Smart Call Home now supported. Adds inventory management etc.

+++ 1.5.1 (2014-05-09)
Bug fixes:
* The transform and field extraction now also works for WLC 8500!

+++ 1.5.0 (2014-05-08)
Features:
* Added lookup file for Cisco System Messages for the following devices:
	- Nexus 7000, MDS 9000
	- Catalyst 2960, 3750 etc
	- Catalyst 4500
	- Catalyst 6500
	- WLC 5500

Make this a dashboard:
sourcetype=cisco:ios | stats count by facility severity_id mnemonic | lookup cisco_ios_messages facility mnemonic OUTPUT vendor_explanation vendor_recommended_action | sort severity_id, -count | table severity_id count facility mnemonic vendor_explanation vendor_recommended_action

There are duplicates. I will review them at a later time

+++ 1.2.2 (2014-04-23)
Features:
* 16 new extractions:
extract_cisco_ios-ILPOWER-3-CONTROLLER_PORT_ERR
extract_cisco_ios-SYS-CPUHOG
extract_cisco_ios-SYS-CPUHOG-2
extract_cisco_ios-LDP-5-SP
extract_cisco_ios-DHCP-6-ADDRESS_ASSIGN
extract_cisco_ios-CLEAR-5-COUNTERS
extract_cisco_ios-OSPF-4-ERRRCV
extract_cisco_ios-CERM-4-RX_TX_BW_LIMIT
extract_cisco_ios-SYS-5-PRIV_I
extract_cisco_ios-UDLD-4-UDLD_PORT_DISABLED
extract_cisco_ios-AUTHMGR-5-SECURITY_VIOLATION
extract_cisco_ios-TRACKING-5-STATE
extract_cisco_ios-RTT-6-SAATHRESHOLD
extract_cisco_ios-EC-5-L3DONTBNDL
extract_cisco_ios-EC-5-PORTDOWN
extract_cisco_ios-EC-5-STAYDOWN

+++ 1.2.1 (2014-02-17)
Features: 
* This app must now be installed on both the search head AND indexer
* We no longer rewrite the indexer to the "ios" index

+++ 1.2.0 (2014-01-09)
Features: Added props, transforms, tags to this app for CIM compliance

+++ 1.0.4 (2013-09-20)
Features: IOS XR support

+++ 1.0.3 (2013-08-12)
Bug fixes: Don't capture ACS events, be stricter on capturing

+++ 1.0.2 (2013-06-07)
Bug fixes:
* Don't capture UCSM events

+++ 1.0.1 (2013-04-23)
Bug fixes:
* Fixed extraction of mnemonic and facility with integers in it

+++ 1.0.0 (2013-03-19)
Features:
* The app has been split up into two parts, one App for the search head and a TA for indexers. This app should be installed on your indexers

++ Application Details

Sourcetype(s):            cisco:ios, Cisco:SmartCallHome  
Supported Technologies:   Cisco IOS, IOS-XE, NX-OS, IOS XR devices


++ Installation Instructions

The Cisco IOS TA can be downloaded, installed, and configured to receive Cisco IOS data by either using the Splunk app setup screen or by manually installing and configuring the app.
This app does not add any new inputs, it merely rewrites syslog events matching the IOS format. You need to already have IOS events coming in as the syslog OR cisco:ios sourcetype.

+++ Setup and configuration

1. Install in $SPLUNK_HOME/etc/apps/TA-cisco_ios

2. Make sure your Cisco devices by default log to one of the following sourcetypes: cisco:ios OR syslog (A regex match will be performed to rewrite the events to the cisco:ios sourcetype)

3. (OPTIONAL for Smart Call Home support)

3.1. OPTIONAL - Add a new TCP data input on a port of your choice, set sourcetype to Cisco:SmartCallHome

3.2. OPTIONAL - On your Cisco devices:
--  
service call-home  
call-home  
 contact-email-addr YOUR.EMAIL@ADDR.ESS  
 site-id "YOUR_SITE_NAME"  
 profile "Splunk"  
  destination transport-method http  
  destination address http http://SPLUNK.SERVER.IP:TCP_PORT_FROM_3.1  
  subscribe-to-alert-group diagnostic severity debug  
  subscribe-to-alert-group environment severity debug  
  subscribe-to-alert-group inventory  
  subscribe-to-alert-group inventory periodic daily 22:30  
--

4. Restart Splunk


++ TODO
* In transforms.conf: NEED TO ADD extract_cisco_ios-general-wlc (8500) and remove the # extraction above. Because time ends up in reported_hostname

++ Getting Help

* Consult Splunk Answers
* Contact the author: mikael@bjerkeland.com

