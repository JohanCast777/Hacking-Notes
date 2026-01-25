
![[Pasted image 20260120121632.png]]

### DOWNLOAD

Download the OP ([Tails](https://tails.net/install/download/index.es.html))

Make an Bootable USB with tails OS
[[🖱🔌💾MAKE AN USB BOOTABLE]]

## First configurations

Keep the default format

![[Pasted image 20260120122625.png]]

Now let's set the tor browser

[[🧅 TOR]]

Use this extra recommendations

[[📟› TERMINAL USAGE TO MORE ANONYMITY]]



💡 KEEP IN MIND!


**Hardware & BIOS**

- Disable Secure Boot (Security tab)[](https://blogs.halodoc.io/using-tails-for-a-secure-private-browsing-experience/)
- Set BIOS/UEFI password to prevent tampering[](https://www.soshalcare.com/tails-os-a-secure-operating-system-for-privacy/)
- Use a dedicated laptop running only Tails, never booting into another OS
- Consider air-gapped setup for maximum isolation[](https://www.anarsec.guide/posts/tails-best/)

**Tails Boot Configuration**

- Do NOT enable Persistent Storage (amnesic design is paramount)[](https://hwbusters.com/networking/tails-os-master-the-dark-web-like-a-pro/)
- Keep all default settings on Welcome Screen[](https://hwbusters.com/networking/tails-os-master-the-dark-web-like-a-pro/)
- Auto-connect to Tor Network (enabled by default)[](https://www.howtogeek.com/tails-os-privacy-focused-linux-distro/)
- Enable MAC address spoofing (enabled by default)
- Never set an Administration password unless necessary[](https://www.anarsec.guide/posts/tails/)

**Network & Connection**

- Use unidentified public Wi-Fi, never your home network[](https://www.anarsec.guide/posts/tails-best/)
- Vary Wi-Fi locations and access times to prevent pattern detection[](https://www.reddit.com/r/privacy/comments/1lamkg8/my_stepbystep_anonymous_setup_using_tails/)
- Connect through VPN → Tor (at router level) when using home internet[](https://www.anarsec.guide/posts/tails-best/)
- Use Tor Bridges only if Tor is blocked in your region[](https://www.anarsec.guide/posts/tails-best/)
- Disable VPN while in Tails if using public Wi-Fi (Tor handles routing)[](https://www.reddit.com/r/privacy/comments/1lamkg8/my_stepbystep_anonymous_setup_using_tails/)

**Operational Security (OpSec)**

- Never log into personal accounts or provide real information
- Create separate Tails sessions for different activities/identities
- Restart Tails between different online activities (don't mix identities)
- Never use the same pseudonym/identity across multiple sessions[](https://www.anarsec.guide/posts/tails/)
- Keep passwords compartmentalized: one KeePassXC file per project[](https://www.anarsec.guide/posts/tails/)

**File & Data Handling**

- Remove metadata from all files before sharing using MAT (Metadata Anonymization Toolkit)[](https://www.anarsec.guide/posts/tails-best/)-  Do not download or execute files (.exe, .zip)[](https://www.reddit.com/r/privacy/comments/1lamkg8/my_stepbystep_anonymous_setup_using_tails/)
- Open untrusted files in offline mode using Dangerzone[](https://www.anarsec.guide/posts/tails-best/)
- Shut down immediately after opening risky files to prevent malware persistence[](https://www.anarsec.guide/posts/tails-best/)
- Avoid sharing files with embedded metadata (dates, locations, device info)[](https://www.anarsec.guide/posts/tails-best/)    

**Browser & Communication**

- Use only Tor Browser; never install plugins/extensions
[](https://www.reddit.com/r/darknet_questions/comments/1dshz79/how_to_set_up_and_use_tails_for_maximum_anonymity/)- ​
- Enable OTR (Off-The-Record) encryption in Pidgin
- Don't log OTR conversations
- Use OnionShare for anonymous file transfers    
- Use Thunderbird with GPG encryption for secure email[](https://www.linkedin.com/pulse/tails-operating-system-ensuring-privacy-anonymity-denys-spys-30ilf)

**System Updates & Software**

- Update Tails regularly for latest security patches[](https://www.reddit.com/r/darknet_questions/comments/1dshz79/how_to_set_up_and_use_tails_for_maximum_anonymity/)    
- Never install unknown software[](https://www.soshalcare.com/tails-os-a-secure-operating-system-for-privacy/)
- Use only pre-installed applications configured for anonymity

**Physical Security**
- Remove USB drive immediately after shutdown—this erases all traces[](https://www.reddit.com/r/privacy/comments/1lamkg8/my_stepbystep_anonymous_setup_using_tails/)
- Protect against keyloggers or BIOS attacks (Tails cannot defend against compromised hardware)[](https://blogs.halodoc.io/using-tails-for-a-secure-private-browsing-experience/)​
- Store USB securely when not in use[](https://www.soshalcare.com/tails-os-a-secure-operating-system-for-privacy/)​

**Critical Limitations**

- Tails cannot protect against compromised hardware, keyloggers, or BIOS-level attacks[](https://blogs.halodoc.io/using-tails-for-a-secure-private-browsing-experience/)​
- Not suitable for streaming or bandwidth-heavy services[](https://hwbusters.com/networking/tails-os-master-the-dark-web-like-a-pro/)​
- Tor exit nodes could be monitored or compromised[](https://blogs.halodoc.io/using-tails-for-a-secure-private-browsing-experience/)​
- Does not protect against phishing or social engineering attacks