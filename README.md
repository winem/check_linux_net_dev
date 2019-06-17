# check_linux__net_dev

Check Linux network interfaces without SNMP.

I was looking for a check plugin that...
  1. does not use SNMP
  2. provides all available interface metrics (incl. warn and crit thresholds if applicable) as performance data
  3. allows alarming on rx / tx bytes, rx / tx drops and rx / tx errors

So I came up with this little Python3 script. 

## Required modules:
  - argparse
  - json 
  - os
  - sys
  - time

## Dependencies and prerequisites
This script was tested on Ubuntu 16.04 & 18.04 and RedHat / Centos 6 & 7. There are no root privileges required to read from `/proc/net/dev`. 
This script needs a temp file to store the metrics from the last check and compare the delta. Per default, it will use `/tmp/' + args.device + '_check_net_dev.tmp`. You can override this by specifying another file by using `--temp-file` you want to use another location due to any restrictions in your environment.

## Usage
Run `./check_net_dev -h` for a detailed help message and overview of all supported parameters.


## Examples
### Without thresholds
`./check_net_dev -d wlan0 --svc-chk-interval 60` - network device statistics for wlan0
`./check_net_dev -d tun0 --svc-chk-interval 300` - network device statistics for tun0 with a service check interval of 300 seconds

### With thresholds
`./check_net_dev -d wlan0 --svc-chk-interval 60 --tx-bytes-warn 300` - network device statistics for tun0 with a warning threshold for transmitted bytes of 300
`./check_net_dev -d wlan0 --svc-chk-interval 60 --tx-bytes-wanr 300 --rx-bytes-crit 3000 --tx-drops-crit 1000 --tx-errors-warn 100` same as above + additional thresholds


## Roadmap for the next version:
  - generic handling of thresholds for any value 
  - be more user-friendly (i.e. input validation and sanity checks & a warning if warn > crit)
  - additional testing in container
  - review for more robust error and exception handling

