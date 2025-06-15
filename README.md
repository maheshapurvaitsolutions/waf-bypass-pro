# WAF Bypass Pro

[![License](https://img.shields.io/badge/license-Educational%20Use%20Only-red.svg)](LICENSE)
[![Python](https://img.shields.io/badge/python-3.8%2B-blue.svg)](https://python.org)
[![Platform](https://img.shields.io/badge/platform-Linux-green.svg)](README.md)

A comprehensive and advanced Web Application Firewall (WAF) bypass testing tool designed for security professionals and researchers.

## ⚠️ DISCLAIMER

**This tool is for authorized security testing and educational purposes only. Ensure you have proper permission before testing any target system. Unauthorized access to computer systems is illegal.**

## Features

### 🛡️ WAF Detection
- Integration with **wafw00f** for comprehensive WAF fingerprinting
- Custom WAF detection methods
- Support for 20+ popular WAF solutions
- Confidence scoring system

### 🎯 Attack Vectors
- **SQL Injection** (SQLi) payloads
- **Cross-Site Scripting** (XSS) vectors
- **Remote Code Execution** (RCE) attempts
- **Local File Inclusion** (LFI) tests
- **XML External Entity** (XXE) attacks
- **Server-Side Template Injection** (SSTI)

### 🔧 Evasion Techniques
- URL encoding and double encoding
- Case manipulation
- Comment insertion
- Unicode normalization
- Payload fragmentation
- Advanced obfuscation methods

### 📊 Reporting
- Beautiful HTML reports with statistics
- JSON export for automation
- CSV format for data analysis
- Plain text reports
- Detailed bypass analysis

### ⚡ Performance
- Multi-threaded testing
- Configurable request delays
- Proxy support
- Custom headers and User-Agent
- Rate limiting protection

## Installation

### Prerequisites
- Python 3.8 or higher
- Linux environment (tested on Kali Linux)
- wafw00f tool (usually pre-installed on Kali)

### Setup

1. **Clone the repository:**
   ```bash
   git clone https://github.com/maheshapurvaitsolutions/waf-bypass-pro.git
   tar -xvzf waf-bypass-pro.tar.gz
   cd waf-bypass-pro
   ```

2. **Create virtual environment:**
   ```bash
   python3 -m venv venv
   source venv/bin/activate
   ```

3. **Install dependencies:**
   ```bash
   pip install -r requirements.txt
   ```

4. **Verify installation:**
   ```bash
   python3 main.py --help
   ```

## Usage

### Basic Usage

**WAF Detection Only:**
```bash
python3 main.py --detect-waf -t https://example.com
```

**Basic Bypass Testing:**
```bash
python3 main.py -t https://example.com
```

**Specific Attack Type:**
```bash
python3 main.py -t https://example.com --payload-type sqli
```

### Advanced Usage

**Custom Evasion Technique:**
```bash
python3 main.py -t https://example.com -e encoding
```

**Multiple Attack Vectors with Custom Settings:**
```bash
python3 main.py -t https://example.com \
    --payload-type all \
    --threads 20 \
    --delay 1.0 \
    --timeout 15 \
    -f html
```

**Using Proxy:**
```bash
python3 main.py -t https://example.com \
    --proxy http://127.0.0.1:8080 \
    --user-agent "Custom-Agent/1.0"
```

**Custom Payload Testing:**
```bash
python3 main.py -t https://example.com \
    -p "<script>alert('XSS')</script>" \
    -e all
```

### Configuration

Edit `config/default.yaml` to customize:
- HTTP client settings
- Payload configurations
- Evasion techniques
- Reporting options
- Security settings

## Command Line Options

| Option | Description | Example |
|--------|-------------|---------|
| `-t, --target` | Target URL | `-t https://example.com` |
| `-p, --payload` | Custom payload | `-p "' OR 1=1--"` |
| `-m, --method` | HTTP method | `-m POST` |
| `-e, --evasion` | Evasion technique | `-e encoding` |
| `--detect-waf` | WAF detection only | `--detect-waf` |
| `--payload-type` | Attack vector type | `--payload-type sqli` |
| `-o, --output` | Output directory | `-o /tmp/reports` |
| `-f, --format` | Report format | `-f json` |
| `--threads` | Thread count | `--threads 15` |
| `--delay` | Request delay | `--delay 2.0` |
| `--timeout` | Request timeout | `--timeout 20` |
| `--proxy` | Proxy URL | `--proxy http://proxy:8080` |
| `--user-agent` | Custom User-Agent | `--user-agent "Bot/1.0"` |
| `--headers` | Custom headers (JSON) | `--headers '{"X-Test":"1"}'` |
| `-v, --verbose` | Verbose output | `-v` |
| `--config` | Config file path | `--config my-config.yaml` |

## Evasion Techniques

### Available Techniques

1. **Encoding** - URL encoding and variations
2. **Case Manipulation** - Random case changes
3. **Comment Insertion** - HTML/SQL comment injection
4. **Unicode Normalization** - Unicode escape sequences
5. **Fragmentation** - Payload splitting and concatenation
6. **Obfuscation** - Advanced payload transformation

### Custom Evasion

Extend the `EvasionEngine` class in `src/evasion/evasion_engine.py` to add your own techniques.

## Payload Management

### Built-in Payloads

The tool includes extensive payload collections for:
- SQL Injection (18+ variants)
- XSS (18+ vectors)
- RCE (20+ techniques)
- LFI (15+ methods)
- XXE (5+ payloads)
- SSTI (15+ templates)

### Custom Payloads

**Add from file:**
```bash
# JSON format
{
  "sqli": ["' OR 1=1--", "'; DROP TABLE users;--"],
  "xss": ["<script>alert(1)</script>"]
}

# Plain text (one per line)
' OR 1=1--
'; DROP TABLE users;--
```

**Load custom payloads:**
```python
from src.payloads.payload_manager import PayloadManager

payload_mgr = PayloadManager(config, logger)
payload_mgr.load_custom_payloads("custom_payloads.json")
```

## Reports

### Report Types

1. **HTML Report** - Interactive web report with statistics
2. **JSON Report** - Machine-readable format
3. **CSV Report** - Spreadsheet-compatible data
4. **Text Report** - Plain text summary

### Report Contents

- Test metadata (target, timestamp, session ID)
- WAF detection results
- Test statistics (success rate, timing)
- Successful bypasses
- Complete test results
- Payload effectiveness analysis

## Architecture

```
waf-bypass-pro/
├── main.py                 # Main entry point
├── config/                 # Configuration files
├── src/
│   ├── core/              # Core application logic
│   ├── detection/         # WAF detection modules
│   ├── evasion/           # Evasion techniques
│   ├── payloads/          # Payload management
│   └── utils/             # Utilities and helpers
├── wordlists/             # Payload wordlists
├── reports/               # Generated reports
└── tests/                 # Test suite
```

## Contributing

1. Fork the repository
2. Create a feature branch
3. Add your improvements
4. Test thoroughly
5. Submit a pull request

### Development Setup

```bash
# Install development dependencies
pip install -r requirements-dev.txt

# Run tests
python -m pytest tests/

# Code formatting
black src/
flake8 src/
```

## Legal Notice

- This tool is intended for **authorized security testing only**
- Users are responsible for compliance with applicable laws
- The authors assume no liability for misuse
- Always obtain proper authorization before testing

## Supported WAFs

Tested against popular WAF solutions including:
- Cloudflare
- AWS WAF
- Akamai
- Incapsula/Imperva
- Sucuri
- Barracuda
- F5 BIG-IP ASM
- ModSecurity
- And many more...

## License

This project is licensed for educational and authorized testing purposes only. See the LICENSE file for details.

## Support

For issues, questions, or contributions:
- Open an issue on GitHub
- Check the documentation
- Review existing issues and solutions

---

**Remember: With great power comes great responsibility. Use this tool ethically and legally.**

