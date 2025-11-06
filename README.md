# NerdQaxe & CKPool Home Assistant Dashboard

This is a customized Home Assistant dashboard configuration for monitoring a BitAxe-compatible miner (specifically NerdQaxe) in combination with CKPool (eusolo).
It is based on the original BitAxe dashboard for Satoshi Radio, but has been heavily modified to correctly query and display solo miner stats and total pool stats from CKPool.

Vorläufiges Bild:
<img width="1364" height="1128" alt="image" src="https://github.com/user-attachments/assets/3b6bc6ac-b040-41a3-b88f-1770987bd793" />

## Features
- Miner Stats: Displays hashrate (GH/s), power consumption (W), temperature (°C), and fan speed (%) of your NerdQaxe miner
- Efficiency Calculation: Calculates your miner's efficiency (GH/W)
- CKPool Solo Stats: Shows your personal 1-hour hashrate on CKPool (in TH/s)
- CKPool Total Stats: Displays the total hashrate (1h and 7d) of the entire CKPool, as well as the number of users and workers
- Summaries: Counts the number of miners that are online or overheated
- Graphs: Visualizes your live hashrate, your pool hashrate, and the total pool hashrate over time (requires mini-graph-card)

## Prerequisites

### Hardware & Network
- A running Home Assistant instance
- HACS (Home Assistant Community Store) must be installed
- The mini-graph-card must be installed via HACS
- A BitAxe / NerdQaxe miner on the same network with a known, static IP address
- Your CKPool wallet address

### Software
- Home Assistant Core 2023.8.0 or newer
- HACS (Home Assistant Community Store) installed
- Custom Cards Required (install via HACS):
  - mini-graph-card

## ⚠️ Important Notes
- **BACKUP YOUR CONFIG**: Always backup your Home Assistant configuration before making changes
- **NETWORK ACCESS**: Ensure your BitAxe miners have static IP addresses or DHCP reservations
- **POOL SPECIFIC**: This dashboard is designed specifically for CKpool

## Installation Steps

1. Install HACS Card: Go to HACS -> Frontend and install the mini-graph-card.
2. Copy Files:
   -  Copy bitaxe.yaml to your /config directory.
   -  Copy dashboard.yaml (or rename it, e.g., mining_view.yaml).
3. Merge Configurations:
   - secrets.yaml: Add the entries from this secrets.yaml to your existing /config/secrets.yaml. Edit it and enter your miner IP (nerdqaxe_ip) and your wallet address (wallet_address and ckpool_solo_resource).
   - configuration.yaml: Add the entire contents of this configuration.yaml to your existing /config/configuration.yaml. **DO NOT REPLACE!** Ensure you only define rest: and sensor:/template: once (or merge the entries).
4. Check Configuration: In Home Assistant, go to Developer Tools -> Check Configuration and ensure no errors are shown.
5. Restart Home Assistant.
6. Set up the Dashboard:
   - Open a dashboard, click "Edit".
   - Add a new "Manual" card and paste the contents of dashboard.yaml into it.
   - Alternatively: If you are using dashboard.yaml as a view file, include it in your Lovelace setup.

## Customization

### Adding More Miners
1. Add new miner IP to `secrets.yaml`
2. Copy a miner section in `bitaxe.yaml`
3. Update template sensors in `configuration.yaml`
4. Add new cards to dashboard if desired

### Removing Miners
1. Remove or comment out relevant sections
2. Update template sensors accordingly

### Modifying Thresholds
- Overheat detection threshold (default 85°C) can be modified in template sensors
- Graph timeframes can be adjusted in dashboard cards

## Troubleshooting

### Common Issues
1. "Sensor Unavailable"
   - Check miner IP address
   - Verify network connectivity
   - Confirm miner is powered on

2. "Pool Stats Missing"
   - Verify wallet address
   - Check pool API status
   - Confirm miners are actually mining

3. "Graphs Not Showing"
   - Verify mini-graph-card is installed
   - Check entity names match your config

## Contributing
Pull requests are welcome! For major changes, please open an issue first to discuss what you would like to change.

## License
[MIT](./LICENSE)

## Acknowledgments
- CKpool - For a amazing Anonymous Solo Pool: https://eusolo.ckpool.org/
- Thanks to the original Repo Owner: https://github.com/satoshiradio/bitaxe-HAS-dashboard
- [BitAxe Community and Project](https://bitaxe.org/) - For creating this amazing open-source miner
- Satoshi Radio Pool Community - For providing an excellent mining pool and the first draft of the dashboard
- Home Assistant Community - For the platform and support
- Bart Mol (https://x.com/Bart_Mol) - For the initial dashboard development

<img width="891" height="891" alt="shovel_btc_pixelart" src="https://github.com/user-attachments/assets/ec0fd162-f449-4603-838d-dc4182e53e1b" />
