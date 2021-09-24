# Windows-Administration-Hardening-
This assignment covers the Windows operating system and command line by performing basic system administration tasks. PowerShell command-line scripting language is used to create and execute scripts. 

In the introduction to the Windows operating system, I learned Windows-based system administration. This covered the Windows operating system and command line by performing basic system administration tasks. I departed from the standard command line by using the PowerShell command-line scripting language to create and execute scripts. I also manage Active Directory Domain Services and secure a Windows Server domain.


The Scenario for this assignment was as follows:

This homework assignment builds on the Group Policy Objectives activities from the previous class.  We will create domain-hardening GPOs and revisit some PowerShell fundamentals.

For this week's homework, please use the Windows Server machine and Windows 10 machine inside your Azure Windows RDP Host machine.


Steps used to complete task:

Task 1
1.	I created a Group Policy Object that prevents my domain-joined Windows machine from using LLMNR called “No LLMNR”.
2.	In the Group Policy Management Editor, the policy was under the following path: Computer Configuration\Policies\Administrative Templates\Network\DNS Client
3.	I enabled the policy called “Turn Off Multicast Name Resolution” and I enabled this policy.
4.	I exited the Group Policy Management Editor and link the GPO to the “GC Computers” organizational unit I previously created.


Task 2
1.	I went within the Windows Server machine again to create another Group Policy Object called “Account Lockout”
2.	I set parameters for the lockout duration to be 15 minutes, account lockout threshold to 10 invalid logins and set the reset account lockout counter after 15 minutes.
3.	I linked link the GPO to the “GC Computers” organizational unit.


Task 3
1.	Working in the Windows Server machine I created a Group Policy Object  called “PowerShell Logging”.
2.	I enabled the “Turn on Module Logging” by clicking “Show” next to Module Names and entering an asterisk * (wildcard) for the Module Name.
3.	I enabled the “Turn on PowerShell Script Block Logging policy”.

This policy uses the following template to log what is executed in the script block:

$collection = 

   foreach ($item in $collection) {
   
     <Everything here will get logged by this policy>
     
}

I checked the Log script block invocation start/stop events: setting.
  
4.	I enabled the “Turn on Script Execution policy” by setting the “Execution Policy” to Allow all scripts.
5.	I enabled the “Turn on PowerShell Transcription policy”,  I left the Transcript output directory blank (this defaults to the user's ~\Documents directory) and checked the “Include invocation headers” option.
6.	I left the “Set the default source path for Update-Help” policy as Not configured.
7.	I linked this new PowerShell Logging GPO to the GC Computers OU.

  

Task 4: Create a PowerShell script that will enumerate the Access Control List of each file or subdirectory within the current working directory. 
1.	I created a foreach loop:
  
$directory=Get-childitem .\

foreach ($item in $directory) {

	Get-Acl $item
	
}

  
2.	I saved this script in C:\Users\sysadmin\Documents as enum_acls.ps.
  
  
Bonus Task 5 
1.	On the Windows 10 machine I ran gpupdate in an administrative PowerShell window to pull the latest Active Directory changes.
2.	I closed and relaunched PowerShell into an administrative session.
3.	I ran  the enum_acls.ps1 script using the full file path and name.
