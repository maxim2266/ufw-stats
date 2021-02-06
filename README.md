# ufw-stats

[![License: BSD 3 Clause](https://img.shields.io/badge/License-BSD_3--Clause-yellow.svg)](https://opensource.org/licenses/BSD-3-Clause)

Show [ufw](https://wiki.archlinux.org/index.php/Uncomplicated_Firewall) actions since boot,
with ip address information from ARIN database. Firewall actions are sourced from `journalctl`.

#### Usage:
```
▶ ./ufw-stats --help
Usage: ufw-stats [OPTION]...
  Show ufw actions since boot, with ip address information from ARIN database.

Options:
  -j, --json          produce JSON optput instead of plain text
  -o, --output=FILE   direct output to the FILE
  -f, --follow        tail the log (continuously print new entries)
  -n, --num-events=N  show N most recent firewall events
  -h, --help          show this message and exit
```

#### Output

In the default text mode the program produces one record per each firewall action, for example:
```
TS:     2021-02-02 11:01:53.494073+0000
ACTION: BLOCK
PROTO:  UDP
SRC:
  SCOPE:   global
  IF:      n/a
  IP:      213.230.86.36
  PORT:    29960
  HOST:    36.64.uzpak.uz
  NET:     213.230.86.0/24
  NAME:    UZTELECOM-DYNAMIC-CUSTOMERS-CGN
  DESCR:   n/a
  COUNTRY: UZ
DEST:
  SCOPE:   private
  IF:      wlp2s0
  IP:      192.168.0.6
  PORT:    53233
  HOST:    m-desktop
  NET:     192.168.0.0/24
  NAME:    n/a
  DESCR:   n/a
  COUNTRY: n/a
```

In JSON mode the output is a JSON array of records each equivalent to the above, for example:
```JSON
{
  "SRC": {
    "IP": "213.230.86.36",
    "SCOPE": [
      "global"
    ],
    "HOST": "36.64.uzpak.uz",
    "NAME": "UZTELECOM-DYNAMIC-CUSTOMERS-CGN",
    "NET": "213.230.86.0/24",
    "COUNTRY": "UZ",
    "PORT": 29960
  },
  "DST": {
    "IP": "192.168.0.6",
    "SCOPE": [
      "private"
    ],
    "HOST": "m-desktop",
    "NET": "192.168.0.0/24",
    "IF": "wlp2s0",
    "PORT": 53233
  },
  "PROTO": "UDP",
  "TS": "2021-02-02T11:01:53.494073+0000",
  "ACTION": "BLOCK"
}
```
