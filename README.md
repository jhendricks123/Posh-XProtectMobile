# TOPIC
about_Posh-XProtectMobile

# SHORT DESCRIPTION
Milestone XProtect Mobile Server helper module

# LONG DESCRIPTION
This module assists administrators by providing a simple cmdlet, Set-MobileServerCertificate, which simplifies the process of adding or updating the binding for 
Milestone XProtect Mobile Server. This is done via the 'netsh http [add|update] sslcert' command which requires the current IP:Port used for HTTPS communication.

The current HTTPS IP:Port values are retrieved from the VideoOS.MobileServer.Service.exe.config file present in the Mobile Server installation directory.

The installation directory for Milestone XProtect Mobile Server is found in the registry path HKLM:\SOFTWARE\WOW6432Node\Milestone\XProtect Mobile Server\.

# EXAMPLES
If using in conjunction with Posh-ACME, you may use the modules like so...
```powershell
$parameters = @{
    ...
}
New-PACertificate @$parameters | Set-MobileServerCertificate
```
Afterward, you might schedule a task in Windows to execute the following PowerShell daily:

```powershell
Submit-Renewal | Set-MobileServerCertificate
```

Doing so will ensure that the certificate is attempted to be renewed daily, but Posh-ACME will only send a request for a new certificate after 60 days from the date of issue.

Alternatively, you may have some other mechanism for generating and renewing certificates. As long as you have installed your certificate to Cert:\LocalMachine\My 
and it includes the private key, you can pipe the certificate or thumprint into Set-MobileServerCertificate.
```powershell
Get-ChildItem Cert:\LocalMachine\My | ? Subject -like '*mobile.example.com*' | Set-MobileServerCertificate
```

# KEYWORDS
Milestone, XProtect, Mobile Server, Let's Encrypt, Certificate, SSL/TLS

# SEE ALSO
- Project: https://github.com/jhendricks123/Posh-XProtectMobile
- Video Tutorial: https://www.youtube.com/playlist?list=PLKZuMVbJCW3MhfIltEOwYDijFuU-s3Kiu
- Milestone KB: https://supportcommunity.milestonesys.com/SCRedir?art=000016329&lang=en_US
