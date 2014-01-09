Copyright (C) 2013 Mikael Bjerkeland, Datametrix AS. All Rights Reserved.

App:                    Cisco IOS Technology Add-On
Current Version:        1.2.0
Last Modified:          2014-01-09
Splunk Version:         4.2.x, 4.3.x, 5.0.x, 6.x
Author:                 Mikael Bjerkeland

The Cisco IOS Technology Add-On (TA) sets the correct sourcetype used for identifying data from Cisco IOS, IOS-XE, NX-OS, XR
Install this TA on your search head and indexer. Install the "Cisco IOS" app on your search head

This TA defines an index "ios" which is referenced by the Cisco IOS App. Make sure your Splunk user searches this index by default.

Please contact me on Splunk Base if there is anything you would like to see in this app.


++ What's New

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

Sourcetype(s):            cisco:ios
Indexes:		  ios
Supported Technologies:   Cisco IOS, IOS-XE, NX-OS, IOS XR devices


++ Installation Instructions

The Cisco IOS TA can be downloaded, installed, and configured to receive Cisco IOS data by either using the Splunk app setup screen or by manually installing and configuring the app.
This app does not add any new inputs, it merely rewrites syslog events matching the IOS format. You need to already have IOS events coming in as the syslog sourcetype OR as index=ios and sourcetype=cisco:ios

+++ Setup and configuration

1. Install in $SPLUNK_HOME/etc/apps/TA-cisco_ios

2. Make sure your Cisco devices by default log to the syslog sourcetype. This app rewrites the source type to cisco:ios based on Regex matches on your indexer.

3. Restart Splunk


++ TODO
* Add SNMP listener (http://x123.net/howto-cisco-mibs-ubuntu.html)

++ Troubleshooting the app


++ Getting Help

* Contact the author: mikael@bjerkeland.com

