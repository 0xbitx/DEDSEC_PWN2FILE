

<p align="center">
<img src="https://media4.giphy.com/media/26FmPUB5MInUrIjvy/giphy.webp", width="400", height="400">
</p>

<h1 align="center">PWN2FILE</h1>
<h4 align="center">A Linux based tool that disguises your payload as 40+ file formats to silently execute on a Linux system.
</h4>

---

## DESCRIPTION

**PWN2FILE** is an advanced Linux-based red team tool that generates malicious desktop launchers disguised as legitimate files. The tool supports 40+ different file formats across multiple categories including documents, media files, archives, and text files.

**Inspired by APT41's proven social engineering and initial access tradecraft** — specifically their use of spear-phishing campaigns and convincing file lures to deliver first-stage payloads — PWN2FILE demonstrates how sophisticated threat actors leverage user trust and desktop environments to gain initial footholds. APT41 has consistently used file-based lures in their operations, often delivering malicious documents or disguised executables to bypass security awareness training and endpoint protections.

When an unsuspecting victim double-clicks the file, their system interprets it as a `.desktop` application rather than the genuine file it appears to be. The launcher performs **two simultaneous actions**:

1. **Decoy Execution**: Downloads and opens a legitimate file (PDF, image, video, audio, archive, or text) to maintain normal behavior
2. **Payload Delivery**: Silently fetches and executes an attacker-supplied payload in the background

This sophisticated approach allows the payload to run completely undetected while the decoy file captures the victim's attention. The tool is intended for use **only in controlled environments with explicit written permission**.

---

## APT41 Parallels

| APT41 Technique | PWN2FILE Implementation |
| :--- | :--- |
| **Spear-phishing lures** | Uses realistic file icons and metadata to impersonate legitimate documents |
| **Living off the land** | Leverages Linux's native `.desktop` file specification — no custom binaries required |
| **Initial access focus** | Prioritizes gaining the first foothold through user interaction |
| **Evasion of security tools** | Bypasses traditional file-type analysis and email gateway scanning |
| **Global targeting** | Generic file format support makes the tool applicable to any target environment |

---

## Detection Opportunities for SOC Analysts

While PWN2FILE creates convincing lures, defenders can hunt for these indicators:

| Indicator | What to Look For |
| :--- | :--- |
| **.desktop file analysis** | Monitor for newly created `.desktop` files with `Exec=` lines containing suspicious commands (e.g., `curl`, `wget`, `bash -c`, `python -c`) |
| **File type mismatch** | Cross-reference reported file extension (e.g., `.pdf`) with actual MIME type using `file` command |
| **Icon anomalies** | Look for `.desktop` files using high-resolution icons inconsistent with standard desktop themes |
| **Process execution** | Monitor for unusual execution chains originating from desktop environment components (`gio-launch-desktop`, `xdg-open`) |
| **Email gateway** | Scan for inbound `.desktop` files via email (often blocked or quarantined by enterprise gateways) |
| **User awareness** | Train employees to recognize when a file opens a terminal or prompts for credentials unexpectedly |

---

## Key Features

### Multi-Format Disguise
- **40+ supported file formats** across 6 categories
- Authentic file icons
- System default application integration

### Multiple Payload Options
- **Reverse Shells**: 10 different variants (Bash, Python, Zsh, Awk, Telnet, Sqlite3, Socat, Ruby, PHP, Netcat)
- **Metasploit**: linux/x64/meterpreter/reverse_tcp & linux/x64/meterpreter_reverse_https
- **Custom Scripts**: Python, Bash, and Binary (ELF) payloads
- **Customizable**: Bring your own payload files

### Cloud Infrastructure
- **Supabase Integration**: Reliable file hosting with CDN delivery
- **Database Tracking**: Automatic logging of all uploaded files
- **Direct URLs**: Instant payload access without authentication
- **Scalable**: Free tier supports multiple concurrent operations

### Evasion Techniques
- **Temporary Files**: Automatic cleanup after execution
- **Hidden Execution**: No terminal windows or error messages

### Zero-Dependency
- Uses only standard libraries
- No compilation or external tools required
- Cross-desktop environment support (GNOME, KDE, XFCE, etc.)

---

## Supported File Types

| Category | File Extensions | # of Formats |
|----------|----------------|--------------|
| **Documents** | .pdf, .doc, .docx, .xls, .xlsx, .ppt, .pptx | 7 |
| **Images** | .png, .jpg, .jpeg, .gif, .bmp, .webp, .tiff, .svg, .ico | 9 |
| **Videos** | .mp4, .avi, .mkv, .webm, .mov, .wmv, .flv, .mpeg, .3gp, .m4v | 10 |
| **Audio** | .mp3, .wav, .ogg, .flac, .aac, .m4a, .opus, .wma, .aiff, .amr | 10 |
| **Archives** | .zip, .rar, .7z, .tar, .gz, .tgz, .bz2, .tbz2, .xz, .txz, .zst | 11 |
| **Text** | .txt, .log, .conf, .cfg, .ini, .properties, .env, .md, .rst, .json, .csv, .xml, .yaml, .yml | 14 |
| **TOTAL** | | **61+ formats** |

---

## SETUP SUPABASE

   * Go to: https://supabase.com/dashboard/new

<img width="714" height="492" alt="Screenshot_20260505_093635" src="https://github.com/user-attachments/assets/d2a58e19-63bf-4210-adf5-ba09a8a2aca6" />
    
   * Create organization (org, personal)

<img width="722" height="896" alt="Screenshot_20260505_093758" src="https://github.com/user-attachments/assets/eb83c347-bb2f-49d3-94f8-2d08b286faa4" />

   * enable (Enable Data API) and (Automatically expose new tables)

<img width="926" height="540" alt="Screenshot_20260505_093835" src="https://github.com/user-attachments/assets/24b60cfe-da7d-44c9-82b4-b49edcf983f1" />

   * Copy Product URL and Publishable Key

<img width="980" height="617" alt="Screenshot_20260505_093921" src="https://github.com/user-attachments/assets/06c1cec9-f365-4140-b78a-2606f5cb9bf1" />

   * Go to Project Settings
     
<img width="714" height="625" alt="Screenshot_20260505_093948" src="https://github.com/user-attachments/assets/f77b1040-866c-4fa3-8133-e67f882b8199" />
   
   * select API Keys

<img width="1201" height="573" alt="Screenshot_20260505_094048" src="https://github.com/user-attachments/assets/3db41af1-f001-4afb-bcc4-fc7f947e8eac" />

   * Copy Service role secret
     
<img width="675" height="622" alt="Screenshot_20260505_094138" src="https://github.com/user-attachments/assets/57899895-0d1a-4f33-bcbd-6f6c552e9cd3" />

   * Go to Storage
     
<img width="1152" height="486" alt="Screenshot_20260505_094209" src="https://github.com/user-attachments/assets/5a5ea812-2d0f-44f0-954d-b874ace983e4" />
   
   * click New bucket

<img width="571" height="633" alt="Screenshot_20260505_094346" src="https://github.com/user-attachments/assets/4abf1a4f-7537-4dcd-8c45-3458aa398cbf" />

   * Put "data" as the bucket name, enable public bucket, and click Create.

and update your config.json file with your 
Project URL, Publishable key, service role secret

### Example:
```json
{
    "SUPABASE_URL": "https://gqbdetbewhevkksclbfu.supabase.co",
    "SUPABASE_KEY": "sb_publishable_TvQ2jFqzrPfsKC-krVrwqA_g_xjy9GM",
    "SUPABASE_SERVICE_KEY": "eyJHbgcrOeJIUsI2NiIsInR3cCI6IkpXcCJ9.eyJpc311OilzeXBhymFrZSIsInJlZiI6ImdxYmR5dGJld2hpdmtrZWNsYmd14iwicm9sZSI6InNlcnZpY2Vfcm9sZSIs3mlhdCI2MTc3NzkyMDk4OCwiZXhwIjoyMDkzNDk2OTg4fQ.L4wdbD3QgDv2NHlP6ZU53wpI2jlLZ0TQXfq6vy7VB_A"
}
```

### INSTALLATION
    git clone https://github.com/0xbitx/DEDSEC_PWN2FILE.git
    cd DEDSEC_PWN2FILE
    chmod +x dedsec-pwn2file
    ./dedsec-pwn2file
    
### TESTED ON FOLLOWING
* Kali Linux 
* Parrot OS 
  
## Legal Disclaimer

This tool is intended for educational and security research purposes only. Unauthorized usage may be illegal in your jurisdiction. The author is not responsible for any misuse of this tool.
