# Introduction
#### **[FR]**

- Agrégation de listes d'adresses IP malveillantes scindée en fichiers de 131 072 entrées au maximum pour être intégrées dans des pare-feux : Fortinet **__FortiGate__**, Palo Alto, pfSense, OPNsense, IPtables ...
- Adresses IP malveillantes de type **phishing**, **malware** et **C2** (Command & Control) donc à bloquer **UNIQUEMENT** en sortie : dans le sens **LAN > WAN**
- Adresses IP ordonnées en fonction du nombre de listes dans lesquelles elles apparaissent (IP malveillantes apparaissant dans le plus de listes sont donc dans le premier fichier full-aa.txt)
- Mise à jour toutes les **heures**

Fichiers à utiliser (liens dans la partie "Links" ci-dessous) :

- full-outgoing-ip-aa.txt : 131 072 adresses IP les plus malveillantes
- full-outgoing-ip-aX.txt : autres adresses IP malveillantes
- full-outgoing-ip-40k.txt : 40 000 adresses IP les plus malveillantes

#### **[EN]**

- Aggregation of lists of malicious IP addresses split into files of a maximum of 131,072 entries to be integrated into firewalls: Fortinet **__FortiGate__**, Palo Alto, pfSense, OPNsense, IPtables ...
- Malicious IP addresses such as **phishing**, **malware** and **C2** (Command & Control), therefore **ONLY** to be blocked in the **LAN > WAN** direction
- Adresses IP classées selon le nombre de listes dans lesquelles elles apparaissent (malicious IPs appearing most frequently first and therefore at the beginning of the full-aa.txt file)
- Updated every **hour**

Files to use (links in the "Links" section below):

- full-outgoing-ip-aa.txt: 131,072 most malicious IP addresses
- full-outgoing-ip-aX.txt: other malicious IP addresses
- full-outgoing-ip-40k.txt: 40,000 most malicious IP addresses

# Menu:

- [Statistics](https://github.com/romainmarcoux/malicious-outgoing-ip#statistics)
- [FR-EN - Implementation](https://github.com/romainmarcoux/malicious-outgoing-ip#implementation)
- [Files URLs](https://github.com/romainmarcoux/malicious-outgoing-ip#files-urls)
- [Sources](https://github.com/romainmarcoux/malicious-outgoing-ip#sources)
- [Releases Notes](https://github.com/romainmarcoux/malicious-outgoing-ip#releases-notes)
- [To support me](https://github.com/romainmarcoux/malicious-outgoing-ip#to-support-me)
- [Contact](https://github.com/romainmarcoux/malicious-outgoing-ip#contact)

# Statistics
Update of the following table: 2026-02-22 22:36 CEST

| Malicious IP addresses in full-outgoing-ip-a-\*                          | %       | Number of IPs |
| ---------------------------------------------------------- | ------- | ------------- |
| Present in 3 sources and more | 0.65 % | 1 161 |
| Present in 2 sources | 8.43 % | 14 868 |
| Present in 1 source | 90.90 % | 160 254 |
| Total | 100 % | 176 283 |

# Implementation
#### **[FR]**
**Comment intégrer** ces listes dans un **pare-feu** ?
- **FortiGate**
   * Menu "Security Fabric → External Connectors → Create New → IP Address"
   * Prendre une URL dans la partie "Links" ci-dessous
   * Après, les listes peuvent être utilisées dans les "Firewall Policy" avec les objets "**IP Address Threat Feed**"
   * Implémentation de la liste full validée même sur le plus petit boitier FortiGate 40F
   * Plus d'informations : le [tutorial vidéo](https://www.youtube.com/watch?v=cg2fliMQdjo) d'un expert sécurité Fortinet et sur cette [page](https://docs.fortinet.com/document/fortigate/7.0.12/administration-guide/891236/ip-address-threat-feed) de l'aide Fortinet
- **Palo Alto** : [lien](https://docs.paloaltonetworks.com/pan-os/9-1/pan-os-admin/policy/use-an-external-dynamic-list-in-policy/external-dynamic-list). Modèle PA-3200 et supérieurs limités à 150k IP (utilisez uniquement full-aa.txt), modèles inférieurs limités à 50k IP (utilisez le fichier full-40k.txt)
- **Check Point** : [lien](https://support.checkpoint.com/results/sk/sk132193)
- **Sophos** : [lien](https://docs.sophos.com/nsg/sophos-firewall/21.0/Help/en-us/webhelp/onlinehelp/AdministratorHelp/ActiveThreatResponse/ConfigureFeeds/ThirdPartyThreatFeeds/index.html).
- **pfSense** : via le package [pfBlocker-NG](https://docs.netgate.com/pfsense/en/latest/packages/pfblocker.html). Il faut aussi augmenter le nombre maximum d'entrées : voir [ici](https://docs.netgate.com/pfsense/en/latest/firewall/aliases.html#alias-sizing-concerns).
- **OPNsense** : via API ([doc](https://docs.opnsense.org/development/api/core/firewall.html)). Modifier le nombre maximal d'entrées d'un alias : "Firewall -> Settings -> Advanced -> Firewall Maximum Table Entries".
- **IPTables** avec le paquet "ipset" : [tutorial 1](https://www.malekal.com/comment-utiliser-ipset-sur-linux/) [tutorial 2](https://fr-wiki.ikoula.com/fr/Cr%C3%A9er_et_administrer_facilement_une_blacklist_avec_ipset/iptables)

#### **[EN]**
**How to integrate** these lists into a **firewall**?
- **FortiGate**
   * Menu "Security Fabric → External Connectors → Create New → IP Address"
   * Take a URL in the "Links" section below
   * Then, the lists can be used in "Firewall Policy" as "**IP Address Threat Feed**" objects.
   * Implementation of the full list validated even on the smallest FortiGate 40F appliance
   * More information: the [video tutorial](https://www.youtube.com/watch?v=cg2fliMQdjo) from a Fortinet security expert and on this page [Fortinet help page](https://docs.fortinet.com/document/fortigate/7.0.12/administration-guide/891236/ip-address-threat-feed)
- **Palo Alto**: [here](https://docs.paloaltonetworks.com/pan-os/9-1/pan-os-admin/policy/use-an-external-dynamic-list-in-policy/external-dynamic-list). PA-3200 model and above limited to 150k IP (use full-aa.txt only), lower models limited to 50k IP (use full-40k.txt file)
- **Check Point** : [link](https://support.checkpoint.com/results/sk/sk132193)
- **Sophos** : [lien](https://docs.sophos.com/nsg/sophos-firewall/21.0/Help/en-us/webhelp/onlinehelp/AdministratorHelp/ActiveThreatResponse/ConfigureFeeds/ThirdPartyThreatFeeds/index.html).
- **pfSense**: via the package [pfBlocker-NG](https://docs.netgate.com/pfsense/en/latest/packages/pfblocker.html). The maximum number of entries must be increased: see [here](https://docs.netgate.com/pfsense/en/latest/firewall/aliases.html#alias-sizing-concerns).
- **OPNsense**: via API ([doc](https://docs.opnsense.org/development/api/core/firewall.html)). Change the maximum number of entries for an alias: "Firewall -> Settings -> Advanced -> Firewall Maximum Table Entries".
- **IPTables** with the "ipset" package: [tutorial 1](https://www.malekal.com/comment-utiliser-ipset-sur-linux/) [tutorial 2](https://fr-wiki.ikoula.com/fr/Cr%C3%A9er_et_administrer_facilement_une_blacklist_avec_ipset/iptables)

# Files URLs

Full aggregation files:

```
https://raw.githubusercontent.com/romainmarcoux/malicious-outgoing-ip/main/full-outgoing-ip-aa.txt
https://raw.githubusercontent.com/romainmarcoux/malicious-outgoing-ip/main/full-outgoing-ip-ab.txt
```

File of the 40,000 most malicious IPs:

```
https://raw.githubusercontent.com/romainmarcoux/malicious-outgoing-ip/main/full-outgoing-ip-40k.txt
```

# Sources

| Filename                                                | Source | Description |
| ------------------------------------------------------------ | ----------- | ----------- |
| abuse.ch-\* | [link](https://threatfox.abuse.ch/) | Command and Control, RAT, Malware IPs |
| alienvault-precisionsec-\* | [link](https://otx.alienvault.com/pulse/60ece5998a5b54a5ffe75cb4) | Command and Control and Malware IPs |
| cert.ssi.gouv.fr-\* | [link](https://www.cert.ssi.gouv.fr/) | Cybercriminal groups, Malware and Phishing IPs |
| cybercrime-tracker.net-\* | [link](https://cybercrime-tracker.net/) | Command and Control and Malware IPs |
| cybercure.ai-\* | [link](https://www.cybercure.ai/) | Malware IPs |
| digitalside.it-\* | [link](https://osint.digitalside.it/) | Malware IPs |
| drb-ra-\* | [link](https://x.com/drb_ra) | Command and Control IPs |
| inquest.net-\* | [link](https://inquest.net/) | Command and Control and Malware IPs |
| malwarebytes-\* | [link](https://www.malwarebytes.com) | Command and Control, Malware and Phishing IPs |
| mattyroberts.io-\* | [link](https://www.cybercure.ai/) | Attackers, Botnet and Malware IPs |
| sicehice-\* | [link](https://sicehice.com/) | Command and Control IPs |
| threatview.io-\* | [link](https://threatview.io/) | Botnet, C2, Malware and Phishing IPs |
| urlabuse.com-\* | [link](https://urlabuse.com/) | Hacked website, Malware and Phishing IPs |
| urlhaus.abuse.ch-\* | [link](https://urlhaus.abuse.ch/) | Malware IPs |
| ut1-fr | [link](https://dsi.ut-capitole.fr/blacklists/) | Malware and Phishing IPs |
| viriback.com-\* | [link](https://viriback.com/) | Command and Control and Malware IPs |

# Release Notes
- 2025-02-25: New source: malwarebytes
- 2024-08-21: New sources: alienvault-precisionsec, cybercrime-tracker.net, digitalside.it, drb-ra, ut1-fr, viriback.com
- 2024-07-17: New source: inquest.net
- 2024-07-11: New source: urlhaus.abuse.ch
- 2024-07-08: Initial release with first sources: abuse.ch, cert.ssi.gouv.fr, cybercure.ai, mattyroberts.io, sicehice.com, threatview.io and urlabuse.com

# To support me

[![BuyMeACoffee](https://raw.githubusercontent.com/romainmarcoux/romainmarcoux/main/img/buymeacoffee.png 'BuyMeACoffee')](https://buymeacoffee.com/romainmarcoux)
[![Paypal](https://www.paypalobjects.com/en_US/FR/i/btn/btn_donateCC_LG.gif 'Paypal')](https://www.paypal.com/donate/?hosted_button_id=TNPNMMBFVVL8E)

# Contact
#### **[FR]**

Contactez-moi via LinkedIn ([mon profil](https://linkedin.com/in/romainmarcoux/)) pour :
- m'indiquer des faux positifs
- être notifié quand un **nouveau segment** de fichier est créé (pour l'ajouter dans votre pare-feu)
- me proposer d'ajouter une **autre** source d'adresses IP malveillantes (voir [sources](https://github.com/romainmarcoux/malicious-ip#sources) actuelles)

#### **[EN]**

Contact me via LinkedIn ([my profile](https://linkedin.com/in/romainmarcoux/)) to:
- notify me false positives
- be notified when a **new file** segment is created (to add it to your firewall)
- suggest I add **another** source of malicious IP addresses (see current [sources](https://github.com/romainmarcoux/malicious-ip#sources)
