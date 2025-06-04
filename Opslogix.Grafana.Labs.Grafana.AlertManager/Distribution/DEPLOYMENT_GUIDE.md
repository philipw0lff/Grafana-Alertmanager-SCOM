# SCOM Management Pack Deployment Guide

## Grafana Alertmanager SCOM Management Pack

This package contains the built Management Pack files for integrating Grafana Alertmanager with System Center Operations Manager (SCOM).

## Package Contents

### Management Pack Files (.mp)
- `Opslogix.Grafana.Labs.Grafana.Alertmanager.mp` - Main Management Pack
- `Opslogix.Grafana.Labs.Presentation.mp` - Presentation/UI components
- `Grafana.Monitoring.mp` - Additional monitoring components

### Management Pack Bundle Files (.mpb)
- `Opslogix.Grafana.Labs.Grafana.AlertManager.mpb` - Main sealed Management Pack bundle
- `Opslogix.Grafana.Labs.Presentation.mpb` - Presentation sealed bundle
- `Grafana.Monitoring.mpb` - Monitoring sealed bundle

## Installation Instructions

### Prerequisites
- SCOM 2016 or later
- Grafana 9.x or later with API access
- Windows Server running SCOM Management Server
- .NET Framework 4.7.2 or later

### Step 1: Import Management Packs
1. Open SCOM Console
2. Navigate to **Administration** → **Management Packs**
3. Right-click and select **Import Management Pack**
4. Import the following files in order:
   - `Opslogix.Grafana.Labs.Presentation.mpb`
   - `Opslogix.Grafana.Labs.Grafana.AlertManager.mpb`

### Step 2: Configure Authentication
1. Create a Grafana API token in Grafana (`Settings` → `API Keys`)
2. In SCOM Console, create a new Run As Account:
   - Type: Basic Authentication
   - Username: (any value, not used)
   - Password: Your Grafana API token

### Step 3: Configure Resource Pool
1. Navigate to **Administration** → **Resource Pools**
2. Find "Grafana Alertmanager Resource Pool"
3. Set to manual membership
4. Add the server that will connect to Grafana

### Step 4: Configure Run As Profile
1. Navigate to **Administration** → **Run As Configuration** → **Profiles**
2. Find "Grafana Alertmanager Run As Profile"
3. Add your Run As Account to "All targeted objects"
4. Ensure distribution to your Resource Pool server

### Step 5: Add Grafana Instance
Use the PowerShell script provided in the README.md to add your Grafana instance to SCOM monitoring.

## File Descriptions

| File | Purpose |
|------|---------|
| `.mp` files | Unsealed Management Packs for development/customization |
| `.mpb` files | Sealed Management Pack bundles for production deployment |

## Recommended Deployment
For production environments, use the `.mpb` (sealed) files as they are digitally signed and cannot be modified.

## Support
Refer to the main README.md file for detailed configuration instructions and troubleshooting.

## Version Information
- Management Pack Version: 25.5.0.0
- Build Configuration: Debug/Release
- Framework: SCOM MP Framework v7.0.5 