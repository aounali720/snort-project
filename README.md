# Snort and Splunk monitoring lab

An Ubuntu-based lab for collecting network alerts with Snort and reviewing them in Splunk. I used it to learn the steps between an IDS rule, an alert log, a forwarder and a searchable SIEM event.

## Lab notes

1. [Configure Snort](Snort-configuration.md) — define monitored traffic, add TCP/ICMP rules and test them.
2. [Forward the alerts](Splunk-forwarder-and-splunk-enterprise.md) — use Splunk Universal Forwarder to send Snort log data to Splunk Enterprise.
3. [Run Splunk on a cloud VM](Splunk-enterprise-on-cloud.md) — move the Splunk instance to a Civo-hosted Ubuntu server and test the connection.

**Tools:** Snort, Splunk Enterprise, Splunk Universal Forwarder, Ubuntu and VM/cloud networking.

This is a lab walkthrough, not a production-ready SOC deployment. The original commands and screenshots document the versions used at the time; review package paths, network exposure, TLS and authentication before reproducing the setup.
