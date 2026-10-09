# Secure Home Hub evidence review

Evidence reviewed October 9, 2026. My SAIT capstone ran from April–December 2023. I was responsible for security on the Raspberry Pi, working directly with iptables and later using UFW. I worked with a six-person team using a Raspberry Pi 4, Ubuntu 22.04 LTS, touchscreen and USB support, hotspot automation, and SSH/RDP/GitHub workflows. These platform details describe our team project; my individual responsibility was Raspberry Pi security.

## Publication recommendation

Use a separate repository named `secure-home-hub-capstone` if the project is published. Present it as a historical team prototype with a clearly attributed personal security contribution. The existing enterprise infrastructure repository covers a separate project and remains unchanged.

## Source assessment

| Material | Finding | Portfolio treatment |
|---|---|---|
| Kyles Security Tasks.docx | A responsibility statement and scheduled tasks, written largely as planned work | Role context; does not prove task completion |
| UFW Rules and Security Policies.docx | Policy/setup instructions, illustrative MQTT port, and password/audit snippets; no final terminal output | Summarize intended policy; do not claim all examples were deployed |
| UFW Monitor Log Script vs parsing.docx | Comparison of rule-change monitoring and traffic-log parsing; no actual monitoring implementation included | Design/research context |
| User Interface Web Design.docx | Touchscreen specification | Hardware context; does not establish GUI authorship |
| IptablesDemonstration.docx | Scripts, dated rule dumps, several variants, and demonstration instructions | Configuration evidence; demonstration instructions are not successful test results |
| Iptables refinement and troubleshooting.docx | Before/after port-display images and logging investigation | Strong troubleshooting evidence with explicit limits |
| iptablesOutput.docx | Live chain listing and saved configuration screenshots | Strongest retained firewall configuration evidence |
| HomeHub-IPTables and additional Security.docx | Evolving firewall examples and integration discussion | Historical development context, with corrections needed before code reuse |
| Encryption deployment and proof-of-concept documents | Research, proposed steps, and expected outcomes | Research scope; completed encryption not demonstrated |
| Final showcase presentation | Team-level description of networking, GUI, security, and lessons learned | Team context; individual authorship and implementation require separate evidence |
| Assignment Business Canvas.docx | Instructor assignment instructions and marking context | Exclude from portfolio assets |
| PROJ_309_2023_Outline.pdf | Course context; first page visually inspected | Exclude from portfolio assets |
| FOIP Capstone Form.pdf | Administrative consent-form filename; form contents not inspected | Exclude from portfolio assets; do not infer permission from its presence |

Sixteen Word documents were extracted locally for review. Security-related text, selected project context, the final showcase slide text, and relevant embedded images were inspected. This was not an exhaustive review of every source file, video, slide layout, or personal-information field. Raw extracted text and review sheets remain under `work/`, outside the portfolio draft.

## Important technical findings

- **Resume wording:** Snort supports network intrusion detection and traffic analysis, while Scapy provides packet manipulation and analysis. Describing them as malicious-file scanning APIs would blur their roles. Separate any file-scanning component and its evidence before including that claim. [Snort documentation](https://www.snort.org/faq/what-is-snort), [Scapy documentation](https://scapy.readthedocs.io/en/latest/introduction.html).
- **UFW transition:** I recall using UFW after difficulties with iptables. Our final showcase still emphasizes iptables and the retained captures demonstrate iptables use. The exact final configuration and transition sequence are not documented well enough to infer a specific root cause. UFW simplifies configuration of the underlying Linux firewall; it is not evidence that Linux packet filtering was replaced. [Ubuntu firewall documentation](https://documentation.ubuntu.com/server/how-to/security/firewalls/index.html).
- **Rule ordering:** One variant accepts forwarding between two interfaces before the later MAC-address rules. Those later rules cannot restrict traffic that an earlier matching accept rule already permits. This is a source-code review finding, not a new test of the original Pi.
- **SSH:** Some variants contain connection-tracking/recent rules without an explicit accept rule for new SSH sessions. With INPUT default DROP, administration access could fail unless another exception matches. The recent rules count new connection attempts, not verified incorrect passwords. The planned demonstration also uses a different port from the shown rules.
- **Persistence:** Saving to a custom `.v4` path does not establish that startup loads it. The IP-set example saves iptables rules but does not show separate IP-set restoration. [Official IP-set save/restore documentation](https://ipset.netfilter.org/ipset.man.html).
- **Password examples:** The Bash example attempts to test password complexity against shadow data. Ubuntu stores hashes in `/etc/shadow`, so this does not validate the original password's composition. The Python example also passes `input=` to `subprocess.call`, which does not provide that input interface. These examples should not be distributed as working password-policy tools. [Ubuntu password hashing](https://documentation.ubuntu.com/security/security-features/cryptography/password-hashing/), [Python subprocess documentation](https://docs.python.org/3.11/library/subprocess.html).
- **Logging:** An active Elasticsearch service and a Kibana home page were captured, while Filebeat was inactive in another capture. These do not prove successful firewall-event ingestion.
- **Encryption:** The documents record a proposed approach and expected results; they do not include endpoint implementation, key-management evidence, or completed encrypted-traffic validation.

The archived code was not executed. The prototype was not reconstructed or security-tested during this review.

## Selected asset provenance

| Portfolio asset | Original source |
|---|---|
| assets/home-hub-iot-setup.png | SecureHomeHub Pictures/Device+IoT.png |
| assets/raspberry-pi-hardware.png | SecureHomeHub Pictures/Hardware.png |
| assets/iptables-live-rules.png | iptablesOutput.docx embedded image2.png |
| assets/iptables-saved-rules.png | iptablesOutput.docx embedded image3.png |
| assets/port-display-before.png | Iptables refinement and troubleshooting.docx embedded image1.png |
| assets/port-display-after.png | Iptables refinement and troubleshooting.docx embedded image2.png |
| assets/elasticsearch-service.png | Iptables refinement and troubleshooting.docx embedded image5.png |

Selected images were copied without visual changes. No live credentials were identified in this selected set during visual review. This is not a guarantee that the original archive is free of secrets.

## Portfolio scope and possible additions

The selected package contains seven reviewed images, new project summaries, and this evidence assessment. The original team presentation, complete reports, assignment materials, consent form, login image, and videos are excluded. No raw firewall or password-management scripts are distributed.

My responsibility and project dates are reflected in the README. Our shared accomplishments are attributed to the team. Any additional team-authored material should be reviewed for permission and attribution before inclusion.

Future evidence could include final UFW output, controlled successful and denied traffic tests, reboot persistence, or actual firewall-log ingestion. These are optional improvements to the historical record; their absence is stated in the current portfolio.
