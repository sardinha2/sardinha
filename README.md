<h1 align="center">
  <a href="https://github.com/loseys/Oblivion//"><img src="https://i.imgur.com/j1GdgLv.png" width="800" title="Oblivion"></a>
</h1>

[![platforms](https://img.shields.io/badge/platform-windows%20%7C%20linux-blue)](https://github.com/loseys/Oblivion/)
[![version](https://img.shields.io/badge/version-v1.0.0-blue)](https://github.com/loseys/Oblivion/)
[![Python 3.8.6](https://img.shields.io/badge/python-3.8-blue.svg)](https://www.python.org/downloads/release/python-386/)
[![license](https://img.shields.io/badge/license-BSD-blue)](https://github.com/loseys/Oblivion/)

**Oblivion** is a tool focused in real time monitoring of new data leaks, notifying if the credentials of the user has been leak out. It's possible too verify if any credential of user has been leak out before.


<h1 align="left">
  <a href="https://github.com/loseys/Oblivion//"><img src="https://i.imgur.com/9SuF29i.png" width="800" title="Oblivion"></a>
</h1>


<h1 align="left">
  <a href="https://github.com/loseys/Oblivion//"><img src="https://i.imgur.com/uR0yHXj.png" width="800" title="Oblivion"></a>
</h1>

## :cyclone: Oblivion Features

* 💪 CVEs scan
* ☑️ Works with powerful APIs
* 🔗 Works too with Google Dorks
* 🔎 Checks your password in Word Lists
* 👀 Checks the last pastes in Pastebin
* 📄 Output to txt, docx, pdf, xlsx, json, html, xml, db
* 🔒 Output to encrypted files
* 📦 Can send result files to multiples Buckets S3
* 📁 Upload the result files to Google Drive
* 📡 Cab send result files by SSH (work with EC2)
* 📢 Notify by Telegram and e-mail
* 📌 Includes option to hide passwords for demonstrations
* 🕒 Works with scheduled scans
* 🔁 Possible to execute loop scans
---

####  APIs

| Service | Functions | Status |
|-|-|-|
| [HaveIBeenPwned](https://haveibeenpwned.com/) | E-mails and passwords | paid |
| [Scylla.sh](https://scylla.sh/)| Cleartext passwords, hashs and salts, usernames, IPs, domain | free |
| [IntelX.io](https://intelx.io/signup)| Cleartext passwords, hashs and salts, usernames, IPs, domain, Bitcoin Wallets, IBAN | paid |
| [Circl.lu](https://cve.circl.lu/api/)| Checks for new CVEs| free |





-----

##  :tangerine: Usage

```bash
usage: h8mail [-h] [-t USER_TARGETS [USER_TARGETS ...]]
              [-u USER_URLS [USER_URLS ...]] [-q USER_QUERY] [--loose]
              [-c CONFIG_FILE [CONFIG_FILE ...]] [-o OUTPUT_FILE]
              [-bc BC_PATH] [-sk] [-k CLI_APIKEYS [CLI_APIKEYS ...]]
              [-lb LOCAL_BREACH_SRC [LOCAL_BREACH_SRC ...]]
              [-gz LOCAL_GZIP_SRC [LOCAL_GZIP_SRC ...]] [-sf]
              [-ch [CHASE_LIMIT]] [--power-chase] [--hide] [--debug]
              [--gen-config]
              
Email information and password lookup tool

optional arguments:
  -h, --help            show this help message and exit
  -t USER_TARGETS [USER_TARGETS ...], --targets USER_TARGETS [USER_TARGETS ...]
                        Either string inputs or files. Supports email pattern
                        matching from input or file, filepath globing and
                        multiple arguments
  -u USER_URLS [USER_URLS ...], --url USER_URLS [USER_URLS ...]
                        Either string inputs or files. Supports URL pattern
                        matching from input or file, filepath globing and
                        multiple arguments. Parse URLs page for emails.
                        Requires http:// or https:// in URL.
  -q USER_QUERY, --custom-query USER_QUERY
                        Perform a custom query. Supports username, password,
                        ip, hash, domain. Performs an implicit "loose" search
                        when searching locally
  --loose               Allow loose search by disabling email pattern
                        recognition. Use spaces as pattern seperators
  -c CONFIG_FILE [CONFIG_FILE ...], --config CONFIG_FILE [CONFIG_FILE ...]
                        Configuration file for API keys. Accepts keys from
                        Snusbase, WeLeakInfo, Leak-Lookup, HaveIBeenPwned,
                        Emailrep, Dehashed and hunterio
  -o OUTPUT_FILE, --output OUTPUT_FILE
                        File to write CSV output
  -bc BC_PATH, --breachcomp BC_PATH
                        Path to the breachcompilation torrent folder. Uses the
                        query.sh script included in the torrent
  -sk, --skip-defaults  Skips HaveIBeenPwned and HunterIO check. Ideal for
                        local scans
  -k CLI_APIKEYS [CLI_APIKEYS ...], --apikey CLI_APIKEYS [CLI_APIKEYS ...]
                        Pass config options. Supported format: "K=V,K=V"
  -lb LOCAL_BREACH_SRC [LOCAL_BREACH_SRC ...], --local-breach LOCAL_BREACH_SRC [LOCAL_BREACH_SRC ...]
                        Local cleartext breaches to scan for targets. Uses
                        multiprocesses, one separate process per file, on
                        separate worker pool by arguments. Supports file or
                        folder as input, and filepath globing
  -gz LOCAL_GZIP_SRC [LOCAL_GZIP_SRC ...], --gzip LOCAL_GZIP_SRC [LOCAL_GZIP_SRC ...]
                        Local tar.gz (gzip) compressed breaches to scans for
                        targets. Uses multiprocesses, one separate process per
                        file. Supports file or folder as input, and filepath
                        globing. Looks for 'gz' in filename
  -sf, --single-file    If breach contains big cleartext or tar.gz files, set
                        this flag to view the progress bar. Disables
                        concurrent file searching for stability
  -ch [CHASE_LIMIT], --chase [CHASE_LIMIT]
                        Add related emails from hunter.io to ongoing target
                        list. Define number of emails per target to chase.
                        Requires hunter.io private API key if used without
                        power-chase
  --power-chase         Add related emails from ALL API services to ongoing
                        target list. Use with --chase
  --hide                Only shows the first 4 characters of found passwords
                        to output. Ideal for demonstrations
  --debug               Print request debug information
  --gen-config, -g      Generates a configuration file template in the current
                        working directory & exits. Will overwrite existing
                        h8mail_config.ini file
```

-----

## :tangerine: Usage examples

###### Query for a single target

```bash
$ h8mail -t target@example.com
```

###### Query for list of targets, indicate config file for API keys, output to `pwned_targets.csv`
```bash
$ h8mail -t targets.txt -c config.ini -o pwned_targets.csv
```

###### Query a list of targets against local copy of the Breach Compilation, pass API key for [Snusbase](https://snusbase.com/) from the command line
```bash
$ h8mail -t targets.txt -bc ../Downloads/BreachCompilation/ -k "snusbase_token=$snusbase_token"
```

###### Query without making API calls against local copy of the Breach Compilation
```bash
$ h8mail -t targets.txt -bc ../Downloads/BreachCompilation/ -sk
```

###### Search every .gz file for targets found in targets.txt locally, skip default checks

```bash
$ h8mail -t targets.txt -gz /tmp/Collection1/ -sk
```

###### Check a cleartext dump for target. Add the next 10 related emails to targets to check. Read keys from CLI

```bash
$ h8mail -t admin@evilcorp.com -lb /tmp/4k_Combo.txt -ch 10 -k "hunterio=ABCDE123"
```
###### Query username. Read keys from CLI

```bash
$ h8mail -t JSmith89 -q username -k "dehashed_email=user@email.com" "dehashed_key=ABCDE123"
```

###### Query IP. Chase all related targets. Read keys from CLI


```bash
$ h8mail -t 42.202.0.42 -q ip -c h8mail_config_priv.ini -ch 2 --power-chase
```

###### Fetch URL content (CLI + file). Target all found emails


```bash
$ h8mail -u "https://pastebin.com/raw/kQ6WNKqY" "list_of_urls.txt"
```


-----

## :tangerine: Thanks & Credits

* [Snusbase](https://snusbase.com/) for being developer friendly
* [kodykinzie](https://twitter.com/kodykinzie) for making a nice [introduction and walkthrough article](https://null-byte.wonderhowto.com/how-to/exploit-recycled-credentials-with-h8mail-break-into-user-accounts-0188600/) and [video](https://www.youtube.com/watch?v=z8G_vBBHtfA) on installing and using h8mail
* [Leak-Lookup](https://leak-lookup.com/) for being developer friendly
* [Dehashed](https://dehashed.com/) for being developer friendly  
* h8mail's Pypi integration is strongly based on the work of audreyr's [CookieCutter PyPackage](https://github.com/audreyr/cookiecutter-pypackage)
* Logo generated using Hatchful by Shopify
* [Jake Creps](https://twitter.com/jakecreps) for his [h8mail v2 introduction](https://jakecreps.com/2019/06/21/h8mail/)  
* [Alejandro Caceres](https://twitter.com/_hyp3ri0n) for making scylla.sh available. Be sure to [support](https://www.buymeacoffee.com/Eiw47ImnT) him if you can
* [IntelX](https://intelx.io) for being developer friendly

:purple_heart: **h8mail can be found in:**
* [BlackArch Linux](https://blackarch.org/recon.html)
* [Tsurugi DFIR VM](https://tsurugi-linux.org/)
* [CSI Linux](https://csilinux.com)  
* [Trace Labs OSINT VM](https://www.tracelabs.org/trace-labs-osint-vm/)


-----

## :tangerine: Related open source projects
* [WhatBreach](https://github.com/Ekultek/WhatBreach) by Ekultek
* [HashBuster](https://github.com/s0md3v/Hash-Buster) by s0md3v
* [BaseQuery](https://github.com/g666gle/BaseQuery) by g666gle
* [LeakLooker](https://github.com/woj-ciech/LeakLooker) by woj-ciech
* [buster](https://github.com/sham00n/buster) by sham00n
* [Scavenger](https://github.com/rndinfosecguy/Scavenger) by ndinfosecguy
* [pwndb](https://github.com/davidtavarez/pwndb) by davidtavarez


-----

## :tangerine: Notes

* Service providers that wish being integrated can send me an email at `k at khast3x dot club` (PGP friendly)
* h8mail is maintained on my free time. Feedback and war stories are welcomed.
* Licence is BSD 3 clause
* My code is [signed](https://help.github.com/en/articles/signing-commits) with my [Keybase](https://keybase.io/ktx) PGP key. You can get it using:  
```bash
# curl + gpg pro tip: import ktx's keys
curl https://keybase.io/ktx/pgp_keys.asc | gpg --import

# the Keybase app can push to gpg keychain, too
keybase pgp pull ktx
```
___

*If you wish to stay updated on this project:*


<h1 align="center">
  <a href="https://twitter.com/kh4st3x"><img src="https://i.imgur.com/S79Nimd.png" width="420" title="Twitter"></a>
</h1>

