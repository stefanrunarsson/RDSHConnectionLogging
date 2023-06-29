# RDSH Connection Logging

Before using ensure to update the required variables for the site
Requires (to be installed on the RDSH hosts):
 - Either SQLcmd or SQLPowershell 
 - PSTerminalServices powershell module
 - Account to run the scheduled task under (you can use the local system account if desired)
 - WMI permissions must be granted on the RDSH Gateway server to allow the account to query for session info

Note: At the moment it classes both logoffs and disconnects as disconnects
This is due to them both logging event 24, with the logoff event 23 happening before event ID 24
Usually happens too quickly for the script to capture the logoff before the disconnect event and has not been worth checking previous events to compare session IDs



*Setup WMI Permissions*

Run "wmimgmt.msc" to open the WMI management
Open the properties

![image](https://github.com/stefanrunarsson/RDSHConnectionLogging/assets/50282626/69bf14e0-a058-4bca-8b21-367468ff16d1)

Go to the security tab

![image](https://github.com/stefanrunarsson/RDSHConnectionLogging/assets/50282626/72ab7c40-fff1-4552-9718-584510cc1cba)

Browse to the TerminalServices under CIMV2

![image](https://github.com/stefanrunarsson/RDSHConnectionLogging/assets/50282626/b5fc8ff4-1d99-49e6-a332-cf233b0f216c)

Edit the security of both the TerminalServices and the ms_409 folders to grant the account running the scheduled task the "Enable Account" and "Remote Enable" options.
Note: "Enable Account" should likely be inherited via the existing "Authenticated Users" setting.
