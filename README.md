Introduction
============

A collection of scripts and files used to set up Cacti to enable it to monitor an Allot NetEnforcer

This is for my own personal use at the moment so if you are interested in graphing Allot products in Cacti rather send me an email

Instructions
------------

**Install Allot MIBs so that Cacti can resolve OIDs**

    sudo mkdir /usr/share/snmp/mibs && sudo cp ALLOT-* /usr/share/snmp/mibs/

**Add the following line to /etc/snmp/snmp.conf**

    mibs +ALLOT-MIB

**Install MIBs needed by ALLOT-MIB**

    sudo apt-get install snmp-mibs-downloader

**Test whether the system can resolve OIDs**

    snmptranslate -IR -On ALLOT-MIB::alSensorId
    .1.3.6.1.4.1.2603.5.5.18.1.1

**Copy allot_sensors.xml and allot_sw to Cacti snmp_queries directory**

    sudo cp allot_sensors.xml allot_sw.xml /var/www/cacti/resource/snmp_queries

**Import Data Queries in Cacti GUI**

In the Cacti GUI go to console -> import templates -> import template from local file.
Import cacti_data_query_netenforcer_-_sensors.xml and cacti_data_query_netenforcer_-_sw.xml in cacti-dev/sensors-data-query.
Go select devices in Cacti and under 'Associated data queries' select 'NetEnforcer - Sensors', then click 'Create graphs for this host'
