# check_net_dev

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

## Current ideas for further improvements:
  - generic handling of thresholds (i.e. not only if rx bytes > x; but also rx bytes < y)
  - be more user-friendly (i.e. input validation and sanity checks & a warning if warn > crit)
  - additional testing in container
  - review for more robust error and exception handling

## Usage
Run `./check_net_dev -h` for a detailed help message and overview of all supported parameters.
