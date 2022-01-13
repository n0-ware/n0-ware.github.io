# AutoRecon - Tib3rius

[Credit to Tib3rius](https://github.com/Tib3rius/AutoRecon)

Ensure Mandatory Dependencies
```
sudo apt install python3
sudo apt install python3-pip
sudo apt install python3-venv
python3 -m pip install --user pipx
python3 -m pipx ensurepath
sudo apt install seclists
```

Ensure Optional Tool Dependencies
```
sudo apt install seclists curl enum4linux feroxbuster impacket-scripts nbtscan nikto nmap onesixtyone oscanner redis-tools smbclient smbmap snmp sslscan sipvicious tnscmd10g whatweb wkhtmltopdf
```

Install with Pipx
```
sudo pipx install git+https://github.com/Tib3rius/AutoRecon.git
```

Install with Pip
```
sudo python3 -m pip install git+https://github.com/Tib3rius/AutoRecon.git
```

Usage
```
usage: autorecon [-t TARGET_FILE] [-p PORTS] [-m MAX_SCANS] [-mp MAX_PORT_SCANS] [-c CONFIG_FILE] [-g GLOBAL_FILE]
                 [--tags TAGS] [--exclude-tags TAGS] [--port-scans PLUGINS] [--service-scans PLUGINS]
                 [--reports PLUGINS] [--plugins-dir PLUGINS_DIR] [--add-plugins-dir PLUGINS_DIR] [-l [TYPE]]
                 [-o OUTPUT] [--single-target] [--only-scans-dir] [--create-port-dirs] [--heartbeat HEARTBEAT]
                 [--timeout TIMEOUT] [--target-timeout TARGET_TIMEOUT] [--nmap NMAP | --nmap-append NMAP_APPEND]
                 [--proxychains] [--disable-sanity-checks] [--disable-keyboard-control]
                 [--force-services SERVICE [SERVICE ...]] [--accessible] [-v] [--version] [--curl.path VALUE]
                 [--dirbuster.tool {feroxbuster,gobuster,dirsearch,ffuf,dirb}]
                 [--dirbuster.wordlist VALUE [VALUE ...]] [--dirbuster.threads VALUE] [--dirbuster.ext VALUE]
                 [--onesixtyone.community-strings VALUE] [--global.username-wordlist VALUE]
                 [--global.password-wordlist VALUE] [--global.domain VALUE] [-h]
                 [targets ...]

Network reconnaissance tool to port scan and automatically enumerate services found on multiple targets.

positional arguments:
  targets               IP addresses (e.g. 10.0.0.1), CIDR notation (e.g. 10.0.0.1/24), or resolvable hostnames (e.g.
                        foo.bar) to scan.

optional arguments:
  -t TARGET_FILE, --target-file TARGET_FILE
                        Read targets from file.
  -p PORTS, --ports PORTS
                        Comma separated list of ports / port ranges to scan. Specify TCP/UDP ports by prepending list
                        with T:/U: To scan both TCP/UDP, put port(s) at start or specify B: e.g.
                        53,T:21-25,80,U:123,B:123. Default: None
  -m MAX_SCANS, --max-scans MAX_SCANS
                        The maximum number of concurrent scans to run. Default: 50
  -mp MAX_PORT_SCANS, --max-port-scans MAX_PORT_SCANS
                        The maximum number of concurrent port scans to run. Default: 10 (approx 20% of max-scans unless
                        specified)
  -c CONFIG_FILE, --config CONFIG_FILE
                        Location of AutoRecon's config file. Default: ~/.config/AutoRecon/config.toml
  -g GLOBAL_FILE, --global-file GLOBAL_FILE
                        Location of AutoRecon's global file. Default: ~/.config/AutoRecon/global.toml
  --tags TAGS           Tags to determine which plugins should be included. Separate tags by a plus symbol (+) to group
                        tags together. Separate groups with a comma (,) to create multiple groups. For a plugin to be
                        included, it must have all the tags specified in at least one group. Default: default
  --exclude-tags TAGS   Tags to determine which plugins should be excluded. Separate tags by a plus symbol (+) to group
                        tags together. Separate groups with a comma (,) to create multiple groups. For a plugin to be
                        excluded, it must have all the tags specified in at least one group. Default: None
  --port-scans PLUGINS  Override --tags / --exclude-tags for the listed PortScan plugins (comma separated). Default:
                        None
  --service-scans PLUGINS
                        Override --tags / --exclude-tags for the listed ServiceScan plugins (comma separated). Default:
                        None
  --reports PLUGINS     Override --tags / --exclude-tags for the listed Report plugins (comma separated). Default: None
  --plugins-dir PLUGINS_DIR
                        The location of the plugins directory. Default: ~/.config/AutoRecon/plugins
  --add-plugins-dir PLUGINS_DIR
                        The location of an additional plugins directory to add to the main one. Default: None
  -l [TYPE], --list [TYPE]
                        List all plugins or plugins of a specific type. e.g. --list, --list port, --list service
  -o OUTPUT, --output OUTPUT
                        The output directory for results. Default: results
  --single-target       Only scan a single target. A directory named after the target will not be created. Instead, the
                        directory structure will be created within the output directory. Default: False
  --only-scans-dir      Only create the "scans" directory for results. Other directories (e.g. exploit, loot, report)
                        will not be created. Default: False
  --create-port-dirs    Create directories for ports within the "scans" directory (e.g. scans/tcp80, scans/udp53) and
                        store results in these directories. Default: True
  --heartbeat HEARTBEAT
                        Specifies the heartbeat interval (in seconds) for scan status messages. Default: 60
  --timeout TIMEOUT     Specifies the maximum amount of time in minutes that AutoRecon should run for. Default: None
  --target-timeout TARGET_TIMEOUT
                        Specifies the maximum amount of time in minutes that a target should be scanned for before
                        abandoning it and moving on. Default: None
  --nmap NMAP           Override the {nmap_extra} variable in scans. Default: -vv --reason -Pn
  --nmap-append NMAP_APPEND
                        Append to the default {nmap_extra} variable in scans. Default: -T4
  --proxychains         Use if you are running AutoRecon via proxychains. Default: False
  --disable-sanity-checks
                        Disable sanity checks that would otherwise prevent the scans from running. Default: False
  --disable-keyboard-control
                        Disables keyboard control ([s]tatus, Up, Down) if you are in SSH or Docker.
  --force-services SERVICE [SERVICE ...]
                        A space separated list of services in the following style: tcp/80/http tcp/443/https/secure
  --accessible          Attempts to make AutoRecon output more accessible to screenreaders. Default: False
  -v, --verbose         Enable verbose output. Repeat for more verbosity.
  --version             Prints the AutoRecon version and exits.
  -h, --help            Show this help message and exit.

plugin arguments:
  These are optional arguments for certain plugins.

  --curl.path VALUE     The path on the web server to curl. Default: /
  --dirbuster.tool {feroxbuster,gobuster,dirsearch,ffuf,dirb}
                        The tool to use for directory busting. Default: feroxbuster
  --dirbuster.wordlist VALUE [VALUE ...]
                        The wordlist(s) to use when directory busting. Separate multiple wordlists with spaces. Default:
                        ['/usr/share/seclists/Discovery/Web-Content/common.txt', '/usr/share/seclists/Discovery/Web-
                        Content/big.txt', '/usr/share/seclists/Discovery/Web-Content/raft-large-words.txt']
  --dirbuster.threads VALUE
                        The number of threads to use when directory busting. Default: 10
  --dirbuster.ext VALUE
                        The extensions you wish to fuzz (no dot, comma separated). Default: txt,html,php,asp,aspx,jsp
  --onesixtyone.community-strings VALUE
                        The file containing a list of community strings to try. Default:
                        /usr/share/seclists/Discovery/SNMP/common-snmp-community-strings-onesixtyone.txt

global plugin arguments:
  These are optional arguments that can be used by all plugins.

  --global.username-wordlist VALUE
                        A wordlist of usernames, useful for bruteforcing. Default: /usr/share/seclists/Usernames/top-
                        usernames-shortlist.txt
  --global.password-wordlist VALUE
                        A wordlist of passwords, useful for bruteforcing. Default:
                        /usr/share/seclists/Passwords/darkweb2017-top100.txt
  --global.domain VALUE
                        The domain to use (if known). Used for DNS and/or Active Directory. Default: None
```

#enumeration #automate