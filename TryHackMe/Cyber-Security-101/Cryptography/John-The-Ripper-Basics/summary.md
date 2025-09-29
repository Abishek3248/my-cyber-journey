# Summary – John the Ripper

**This module introduced practical techniques and workflows for using John the Ripper to identify and crack password hashes.**

- Learned core John modes and when to use them: wordlist (+rules) for most cases, single (username-based mangling), and incremental (brute force) as a last resort.
- Prepared and converted targets for John: unshadow for Linux passwd+shadow, zip2john / rar2john for archives, and ssh2john for private-key passphrases.
- Learned to identify and force formats (--list=formats and --format=) when auto-detection is unreliable.
- Used and customised rule sets (via john.conf) to boost wordlist attacks with mangling rules.
- Managed results with the pot file and john --show to list cracked plaintexts and mappings.
- Best-practice workflow: identify format → wordlist + rules (force format if needed) → tune rules → fallback to incremental.
- Tooling guidance: use local helpers (e.g., hash-id) and prefer John on CPU/VM when appropriate; combine knowledge of other tools (e.g., Hashcat for GPU-accelerated cracking) when needed.

**This room focused on practical, repeatable steps for preparing hashes, selecting attack modes, and efficiently extracting plaintexts using John the Ripper.**
