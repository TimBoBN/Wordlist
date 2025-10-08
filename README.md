# FFUF Wordlists Collection

A comprehensive collection of specialized wordlists for web application security testing and bug bounty hunting using [ffuf](https://github.com/ffuf/ffuf).

## 📋 Overview

This repository contains curated wordlists optimized for discovering sensitive files, endpoints, and configurations during web application penetration testing. Each wordlist is carefully organized by category for efficient and targeted fuzzing.

## 📂 Wordlists

### Complete Collection
- **`wordlist_files.txt`** - Master wordlist containing all entries from specialized lists

### Specialized Lists

| Wordlist | Description | Use Case |
|----------|-------------|----------|
| `wordlist_backups.txt` | Backup files, database dumps, archives | Finding `.bak`, `.old`, `.backup`, `.sql`, compressed backups |
| `wordlist_apis.txt` | API endpoints and documentation | Discovering Swagger, GraphQL, REST APIs, OpenAPI specs |
| `wordlist_cloud.txt` | Cloud and container configurations | AWS, Azure, GCP credentials, Docker, Kubernetes configs |
| `wordlist_logs.txt` | Log files and monitoring data | Access logs, error logs, debug files, rotated logs |
| `wordlist_cms.txt` | CMS-specific paths | WordPress, Joomla, Drupal admin panels, plugins, themes |

## 🚀 Usage

### Basic ffuf Usage

```bash
# Scan with complete wordlist
ffuf -u https://target.com/FUZZ -w wordlist_files.txt

# Scan for backups only
ffuf -u https://target.com/FUZZ -w wordlist_backups.txt

# Scan for API endpoints
ffuf -u https://target.com/api/FUZZ -w wordlist_apis.txt

# Match only 200 status codes
ffuf -u https://target.com/FUZZ -w wordlist_files.txt -mc 200

# Filter out specific status codes
ffuf -u https://target.com/FUZZ -w wordlist_files.txt -fc 404,403
```

### Advanced Examples

```bash
# Recursive fuzzing with extensions
ffuf -u https://target.com/FUZZ -w wordlist_backups.txt -recursion -recursion-depth 2 -e .php,.html,.txt

# Multiple wordlists (directory + file)
ffuf -u https://target.com/FUZZ/FUZ2Z -w wordlist_dirs.txt:FUZZ -w wordlist_files.txt:FUZ2Z

# With custom headers
ffuf -u https://target.com/FUZZ -w wordlist_apis.txt -H "Authorization: Bearer TOKEN"

# Rate limiting (10 requests per second)
ffuf -u https://target.com/FUZZ -w wordlist_files.txt -rate 10

# Silent mode with output
ffuf -u https://target.com/FUZZ -w wordlist_logs.txt -s -o results.json
```

## 🎯 Recommended Scanning Strategy

### 1. Initial Reconnaissance
```bash
ffuf -u https://target.com/FUZZ -w wordlist_files.txt -mc 200,301,302,401,403 -o initial_scan.json
```

### 2. Targeted Scans Based on Technology Stack

**For WordPress Sites:**
```bash
ffuf -u https://target.com/FUZZ -w wordlist_cms.txt -mc 200,301,302
```

**For API Services:**
```bash
ffuf -u https://target.com/FUZZ -w wordlist_apis.txt -mc 200,401
```

**For Cloud Applications:**
```bash
ffuf -u https://target.com/FUZZ -w wordlist_cloud.txt -mc 200,403
```

### 3. Deep Dive for Sensitive Files
```bash
ffuf -u https://target.com/FUZZ -w wordlist_backups.txt -mc all -fc 404
ffuf -u https://target.com/FUZZ -w wordlist_logs.txt -mc all -fc 404
```

## ⚠️ Important Notes

### Legal Disclaimer
- **Only use these wordlists on systems you have explicit permission to test**
- Unauthorized access to computer systems is illegal
- Always follow responsible disclosure practices
- Respect bug bounty program rules and scope

### Rate Limiting
- Use `-rate` flag to avoid overwhelming targets
- Respect `robots.txt` and rate limits
- Consider using `-delay` for slower, stealthier scans

### False Positives
- Always manually verify findings
- Check for honeypots and decoy files
- Validate actual vulnerability before reporting

## 🛠️ Customization

### Creating Custom Lists
```bash
# Combine multiple lists
cat wordlist_backups.txt wordlist_logs.txt > wordlist_sensitive.txt

# Remove duplicates
sort -u wordlist_files.txt > wordlist_unique.txt

# Filter by extension
grep "\.sql$" wordlist_backups.txt > wordlist_sql_only.txt
```

### Adding Your Own Entries
Feel free to fork and customize these wordlists for your specific needs. Common additions:
- Company-specific naming conventions
- Technology-specific paths
- Custom backup formats
- Internal tool endpoints

## 📊 Statistics

- **Total entries in complete list:** ~4,500+
- **Backup patterns:** 200+
- **API endpoints:** 150+
- **Cloud configurations:** 100+
- **Log file patterns:** 300+
- **CMS paths:** 180+

## 🤝 Contributing

Contributions are welcome! If you have suggestions for additional entries:

1. Fork the repository
2. Add your entries to the appropriate wordlist
3. Remove duplicates: `sort -u wordlist_name.txt -o wordlist_name.txt`
4. Submit a pull request with a description of additions

### Contribution Guidelines
- One entry per line
- No empty lines
- Relevant to the wordlist category
- Actually useful for security testing
- No obvious honeypot patterns

## 📚 Resources

- [ffuf Official Documentation](https://github.com/ffuf/ffuf)
- [OWASP Testing Guide](https://owasp.org/www-project-web-security-testing-guide/)
- [Bug Bounty Methodology](https://www.bugbountyhunter.com/)
- [SecLists Project](https://github.com/danielmiessler/SecLists)

## 🔄 Updates

This repository is actively maintained. Check back regularly for updates and new wordlists.

Last updated: 2025

## 📝 License

This project is licensed under the MIT License - see the LICENSE file for details.

## ⭐ Acknowledgments

- Inspired by SecLists and other wordlist projects
- Community contributions and feedback
- Bug bounty hunters and security researchers

---

**Happy Hunting! 🎯**

*Remember: With great power comes great responsibility. Always test ethically.*
