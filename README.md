# Solana Profit Tracker

## Project Objectives
- Utilize APIs, blockchain data, and WebSocket connections to analyze transactions.
- Identify wallets that have achieved significant profits (PNL).
- Monitor these wallets to determine which tokens to buy and develop strategies based on their activities.

A real-time monitoring tool for Solana DEX activities using direct Solana CLI integration.

## Features

- Real-time monitoring of multiple DEX programs on Solana
- Direct integration with Solana CLI for reliable data access
- Live web interface for monitoring new tokens and pairs
- WebSocket-based real-time updates
- Configurable monitoring parameters
- Transaction analysis and logging
- Data export in multiple formats (CSV, JSON)
- Activity summaries and reports
- Support for multiple popular DEXes (Serum, Raydium, Orca)
- Known token database with automatic metadata resolution

## Prerequisites

- Solana CLI tools
- PowerShell 7 (for Windows users)

## Installation

1. Clone the repository:
```bash
git clone https://github.com/yourusername/dexlive-monitor.git
cd dexlive-monitor
```

2. Build the project:
```bash
cargo build --release
```

The executable will be available in `target/release/dexlive-monitor`

## Web Interface

The monitor includes a modern web interface accessible at `http://localhost:3030` when running. Features include:

- Real-time token pair monitoring
- Live updates via WebSocket connection
- Token information display including:
  - Token symbol and name
  - Token address
  - Decimals and supply information
  - Discovery timestamp
- Modern, responsive design similar to popular DEX monitoring tools

## Configuration

The monitor can be configured through both a config file and command-line arguments. Create a `config.json` file or use the default one that will be created on first run.

Example `config.json`:
```json
{
  "rpc_url": "https://api.mainnet-beta.solana.com",
  "update_frequency": 5,
  "dex_programs": [
    {
      "name": "Serum DEX v3",
      "program_id": "9xQeWvG816bUx9EPjHmaT23yvVM2ZWbrrpZb9PusVFin",
      "enabled": true
    },
    {
      "name": "Raydium AMM v4",
      "program_id": "675kPX9MHTjS2zt1qfr1NYHuzeLXfQM9H24wFSUt1Mp8",
      "enabled": true
    },
    {
      "name": "Orca Whirlpools",
      "program_id": "whirLbMiicVdio4qvUfM5KAg6Ct8VwpYzGff3uctyCc",
      "enabled": true
    }
  ]
}
```

## Cas d'utilisation

- **Surveillance des nouvelles paires de tokens**: Utilisez DEXLive Monitor pour suivre les nouvelles paires de tokens sur les DEX en temps réel, ce qui vous permet de réagir rapidement aux opportunités du marché.

- **Analyse des transactions**: Analysez les transactions pour identifier les tendances du marché et prendre des décisions éclairées sur vos investissements.

- **Exportation des données**: Exportez les données d'activité pour des rapports ou des analyses externes, facilitant ainsi le suivi des performances.

## Exemples d'utilisation

### Exemple de configuration pour surveiller un DEX spécifique
Pour surveiller le DEX Serum, vous pouvez utiliser le fichier de configuration suivant :

```json
{
  "rpc_url": "https://api.mainnet-beta.solana.com",
  "update_frequency": 5,
  "dex_programs": [
    {
      "name": "Serum DEX v3",
      "program_id": "9xQeWvG816bUx9EPjHmaT23yvVM2ZWbrrpZb9PusVFin",
      "enabled": true
    }
  ]
}
```

### Commandes pour exporter des données
Pour exporter les données d'activité d'une date spécifique, utilisez la commande suivante :

```bash
dexlive-monitor export --date 20231201
```

Pour générer un résumé des activités d'une date spécifique, utilisez :

```bash
dexlive-monitor summary --date 20231201
```

### Monitor DEX Activity (Default)
```bash
dexlive-monitor
```

This will start both the monitoring service and the web interface. You can access the web interface at `http://localhost:3030`.

With custom configuration:
```bash
dexlive-monitor --config custom_config.json --rpc-url https://your-rpc-url --frequency 10
```

### Export Data
Export activity data for a specific date:
```bash
# Export as CSV (default)
dexlive-monitor export --date 20231201

# Export as JSON
dexlive-monitor export --date 20231201 --format json

# Export specific program activity
dexlive-monitor export --date 20231201 --program 9xQeWvG816bUx9EPjHmaT23yvVM2ZWbrrpZb9PusVFin
```

### View Activity Summary
Generate a summary of activities for a specific date:
```bash
dexlive-monitor summary --date 20231201
```

### Command-line Options
- `--config, -c`: Path to config file (default: config.json)
- `--rpc-url, -r`: RPC URL for Solana network (overrides config file)
- `--frequency, -f`: Update frequency in seconds (overrides config file)
- `--log-dir, -l`: Directory for storing activity logs (default: logs)

### Subcommands
- `monitor`: Start monitoring DEX activity and web interface (default)
- `export`: Export activity data
  - `--date, -d`: Date to export (YYYYMMDD format)
  - `--format, -f`: Export format (csv or json)
  - `--program, -p`: Filter by program ID
- `summary`: Show activity summary
  - `--date, -d`: Date to summarize (YYYYMMDD format)

## Output

The monitor creates daily log files in JSON format under the specified log directory and provides real-time updates through the web interface. Each log entry contains:
- Timestamp
- Program name
- Program ID
- Transaction signature
- Transaction type
- Detailed information

### Export Formats
- CSV: Comma-separated values format, suitable for spreadsheet applications
- JSON: Structured format, suitable for programmatic analysis
- Summary: Text-based overview of daily activities

Export files are stored in the `logs/exports` directory with filenames following the pattern:
- CSV: `dex_activity_YYYYMMDD.csv`
- JSON: `dex_activity_YYYYMMDD.json`
- Program-specific: `dex_activity_YYYYMMDD_PROGRAMID.{csv|json}`

## Development

To run tests:
```bash
cargo test
```

To run with debug logging:
```bash
$env:RUST_LOG="debug"  # PowerShell
./target/release/dexlive-monitor
```

## Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## License

This project is licensed under the MIT License - see the LICENSE file for details.
