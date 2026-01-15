<p align="center">
  <img src="https://raw.githubusercontent.com/lucasbazan/SentinelOnion/refs/heads/main/assets/SentinelOnionLogo.png" alt="SentinelOnion Logo" width="400"/>
</p>

**SentinelOnion** is a modular framework for **discovery, crawling, and analysis of Deep/Dark Web content**, with multi-network support and native integration with **YARA**, **Regex**, and **keyword-based search**.

<p align="center">
  <a href="https://sonarcloud.io/summary/new_code?id=lucasbazan_SentinelOnion">
    <img src="https://sonarcloud.io/api/project_badges/quality_gate?project=lucasbazan_SentinelOnion" alt="Quality gate"/>
  </a>
  &nbsp;&nbsp;&nbsp;
  <a href="https://github.com/lucasbazan/SentinelOnion/actions/workflows/ggshield.yml">
    <img src="https://github.com/lucasbazan/SentinelOnion/actions/workflows/ggshield.yml/badge.svg?branch=main" alt="GitGuardian"/>
  </a>
  &nbsp;&nbsp;&nbsp;
  <a href="https://github.com/lucasbazan/SentinelOnion/actions/workflows/semgrep.yml">
    <img src="https://github.com/lucasbazan/SentinelOnion/actions/workflows/semgrep.yml/badge.svg" alt="Semgrep (SAST)"/>
  </a>
</p>


---

## 🌌 Supported Networks
[![FOSSA Status](https://app.fossa.com/api/projects/git%2Bgithub.com%2Flucasbazan%2Fsentinelonion.svg?type=shield)](https://app.fossa.com/projects/git%2Bgithub.com%2Flucasbazan%2Fsentinelonion?ref=badge_shield)


- **Tor (.onion)**
- **I2P (.i2p)**
- **Freenet**
- **GNUnet (.zkey)**
- **Lokinet (.loki)**
- **ZeroNet**

---

## ⚙️ Architecture

```bash
sentinelonion/
├── core/ # main engine
├── rules/ # YARA + Regex
├── networks/
│ ├── tor.py # Tor driver
│ ├── i2p.py # I2P driver
│ ├── freenet.py # Freenet driver
│ ├── gnunet.py # GNUnet driver
│ ├── lokinet.py # Lokinet driver
│ ├── zeronet.py # ZeroNet driver
└── outputs/ # results export (JSON, Prometheus, ELK)
```

---

## 🚀 Installation

### Requirements
- Python 3.10+
- Docker

### Setup
```bash
git clone https://github.com/lucasbazan/SentinelOnion.git
cd SentinelOnion
pip install -r requirements.txt
```

---

## 🔍 Usage

1. Discover websites in search engines

Query directories and search engines from the selected networks and store results in a file:
```bash
python3 main.py discover --network tor,i2p --keywords "drugs,market" --output websites.txt
```
This will generate websites.txt with the discovered URLs.

2. Crawl and analyze websites

Load websites from a list and apply YARA/Regex detection:
```bash
python3 main.py crawl --input websites.txt
```

Or crawl a single URL:
```bash
python3 main.py crawl --url http://example.onion
```

Or via pipe (stdin):
```bash
echo "http://example.onion" | python3 main.py crawl
```

3. Export results to JSON or CSV

```bash
python3 main.py crawl --input websites.txt --output results[.json|.csv]
```

---

🧾 YARA & Regex Rules

Custom detection rules are stored in the rules/ folder.
You can add your own rules to detect:

- Cryptocurrency wallets
- Emails
- Usernames
- Credentials
- Any custom pattern

Example (Bitcoin wallet detection):

```yara
rule Bitcoin_Wallet {
  strings:
    $btc = /[13][a-km-zA-HJ-NP-Z1-9]{25,34}/
  condition:
    $btc
}
```

---

📊 Integrations

- Export results to JSON and CSV
- Expose metrics to Prometheus
- Integrate with ELK (Elasticsearch + Kibana)

---

🛣️ Roadmap

- ☐ Tor support
- ☐ Discovery mode (discover)
- ☐ Crawling mode (crawl)
- ☐ I2P support
- ☐ Freenet support
- ☐ GNUnet support
- ☐ Lokinet support
- ☐ ZeroNet support
- ☐ Dashboard for visualization

---

⚠️ Legal Disclaimer

SentinelOnion is a tool created for academic research, security studies, and digital forensics.
It must not be used for illegal activities. The author is not responsible for misuse.


## License
[![FOSSA Status](https://app.fossa.com/api/projects/git%2Bgithub.com%2Flucasbazan%2Fsentinelonion.svg?type=large)](https://app.fossa.com/projects/git%2Bgithub.com%2Flucasbazan%2Fsentinelonion?ref=badge_large)