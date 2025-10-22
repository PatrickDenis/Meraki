Meraki Switch Port Exporter

This script automates the collection of detailed Meraki switch port data — including VLANs, MAC addresses, vendors, and CDP/LLDP neighbors — into organized CSV files.
It’s particularly useful because the Meraki Dashboard does not natively allow full switch port exports with this level of granularity or flexibility.
Why Use This Script?

Cisco Meraki’s web GUI is great for monitoring but limited for bulk data handling.
From the GUI, you can’t easily:

    Export switch port data with MAC/OUI, VLAN, and neighbor details at once.
    Correlate client MAC addresses with port names automatically.
    Generate unified reports across multiple switches or entire networks.

This script bridges that gap by using the Meraki Dashboard API, allowing you to:

    Automate switch inventory collection for audits, troubleshooting, or documentation.
    Generate per-switch CSV files as well as one combined master export.
    Enhance visibility into which clients are connected to which ports, their vendors, and their uplink neighbors.

It’s a must-have for network administrators, auditors, and engineers who need detailed switch visibility and prefer command-line control.
