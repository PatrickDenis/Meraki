# Meraki Switch Port Exporter

This script automates the collection of detailed **Meraki switch port data** — including VLANs, MAC addresses, vendors, and CDP/LLDP neighbors — into organized CSV files.  
It’s particularly useful because **the Meraki Dashboard does not natively allow full switch port exports** with this level of granularity or flexibility.

---

## Why Use This Script?

Cisco Meraki’s web GUI is great for monitoring but limited for bulk data handling.  
From the GUI, you can’t easily:

- Export switch port data with MAC/OUI, VLAN, and neighbor details at once.  
- Correlate client MAC addresses with port names automatically.  
- Generate unified reports across multiple switches or entire networks.

This script bridges that gap by using the **Meraki Dashboard API**, allowing you to:
- **Automate switch inventory collection** for audits, troubleshooting, or documentation.
- **Generate per-switch CSV files** as well as one combined master export.
- **Enhance visibility** into which clients are connected to which ports, their vendors, and their uplink neighbors.

It’s a must-have for **network administrators, auditors, and engineers** who need detailed switch visibility and prefer command-line control.

---

## Requirements

Make sure your system meets these prerequisites:

- **Python 3.8+**
- **Meraki Python SDK** (`pip install meraki`)
- A **valid Cisco Meraki API key**
  - Found under **Dashboard → My Profile → API Access → Generate new API key**
- Internet access to connect to the Meraki Cloud API.

---

## Setup Instructions

### 1. Clone or Download the Repository
```bash
git clone https://github.com/PatrickDenis/Meraki.git
cd Meraki
```

### 2. Install Dependencies
```bash
pip install meraki
```

### 3. Configure Your API Key and Switch List
Open the script file (e.g., `meraki_switch_export.py`) and update:

```python
API_KEY = 'YOUR_API_KEY_HERE'
SWITCH_SERIALS = ['QXXX-XXXX-XXXX']
```

You can add multiple switch serials as a list:
```python
SWITCH_SERIALS = ['QXXX-XXXX-XXXX', 'QYYY-YYYY-YYYY', 'QZZZ-ZZZZ-ZZZZ']
```

### 4. Run the Script
```bash
python meraki_switch_export.py
```

The script will automatically:
- Create an output folder named **`meraki_switch_exports`**
- Generate one CSV per switch
- Produce a combined file:  
  `ALL_SWITCHES_COMBINED.csv`

---

## Output Files Explained

| File | Description |
|------|--------------|
| `SwitchName_SERIAL.csv` | Contains per-switch detailed port information |
| `ALL_SWITCHES_COMBINED.csv` | Aggregates all switch data into one master report |
| `meraki_switch_exports/` | Automatically created directory for all reports |

Each CSV includes the following fields:

- **Switch Name**  
- **Port Number**  
- **Port Name**  
- **VLAN**  
- **MAC Address**  
- **OUI Vendor**  
- **CDP/LLDP Neighbor**

These details allow you to **trace connectivity** at every port — useful for documentation, topology mapping, and network cleanup.

---

## How It Works

1. **Authentication:**  
   Connects to your Meraki dashboard using your API key.

2. **Device Discovery:**  
   Retrieves each switch device and its associated network ID.

3. **Data Collection:**  
   - Fetches port configurations and live port statuses.  
   - Gathers connected client data (MAC and vendor).  
   - Merges CDP/LLDP neighbor info for topology insight.

4. **CSV Generation:**  
   Writes data to easy-to-read CSV files for use in Excel, Power BI, or inventory databases.

---

## Benefits of Using the API Instead of the GUI

- **Automation:** Run it daily or on a schedule with cron.  
- **Scalability:** Works across dozens or hundreds of switches.  
- **Customization:** Extend to include PoE, link speed, or port status.  
- **Offline Analysis:** CSV files can be shared or imported anywhere.  
- **Auditing:** Provides a snapshot of network configuration for compliance reviews.

---

## Security Tips

- **Never share your API key publicly.**
- Store your key in an environment variable if you’re automating:
  ```bash
  export MERAKI_API_KEY="your_api_key"
  ```
  And modify your script:
  ```python
  import os
  API_KEY = os.getenv('MERAKI_API_KEY')
  ```

---

## 🧪 Example Output

Example row from CSV:

| Switch Name | Port Number | Port Name | VLAN | MAC Address | OUI Vendor | CDP/LLDP Neighbor |
|--------------|--------------|-----------|-------|---------------|--------------|--------------------|
| Core-Switch-01 | 3 | Office-AP | 30 | 88:36:6C:2A:3F:91 | Cisco Systems | AP-Ceiling-01 |

---

## Troubleshooting

**Issue:** API key error or rate limit  
**Fix:** Ensure your key has full organization access. Retry after a few minutes.

**Issue:** MAC or vendor missing  
**Fix:** The client may not be active or visible to Meraki Cloud.

**Issue:** “Permission denied” on write  
**Fix:** Run from a writable directory or adjust file permissions.

---

## Next Steps

You can easily extend this tool to:
- Push results to a **database or dashboard**
- Integrate with **Grafana or Power BI**
- Add **port status, PoE consumption, or bandwidth usage**

---

## Author

**Patrick Denis**  
Senior Network Engineer • Network Solutions USA  
Fort Lauderdale, FL  

