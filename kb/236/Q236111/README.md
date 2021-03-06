---
layout: page
title: "Q236111: XCLN: Client Cannot Change Windows NT or Windows 2000 Password"
permalink: /kb/236/Q236111/
---

## Q236111: XCLN: Client Cannot Change Windows NT or Windows 2000 Password

{% raw %}

	Article: Q236111
	Product(s): Microsoft Exchange
	Version(s): 2000,4.0,5.0,8.0,8.1,8.2
	Operating System(s): 
	Keyword(s): 
	Last Modified: 11-JUN-2002
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Exchange Macintosh client, versions 4.0, 5.0 
	- Microsoft Exchange Windows NT client, versions 4.0, 5.0 
	- Microsoft Exchange Windows 95/98 client, versions 4.0, 5.0 
	- Microsoft Exchange Windows 3.x client, versions 4.0, 5.0 
	- Microsoft Outlook 2001 for Mac 
	- Microsoft Outlook for Macintosh, Exchange Server Edition, versions 8.0, 8.1, 8.2 
	- Microsoft Outlook 2002 
	- Microsoft Outlook 2000 
	- Microsoft Outlook 98 
	- Microsoft Outlook 97 
	- Microsoft Windows 2000 Advanced Server 
	- Microsoft Windows 2000 Server 
	-------------------------------------------------------------------------------
	
	IMPORTANT: This article contains information about modifying the registry. Before you modify the registry, make sure to back it up and make sure that you understand how to restore the registry if a problem occurs. For information about how to back up, restore, and edit the registry, click the following article number to view the article in the Microsoft Knowledge Base:
	
	  Q256986 Description of the Microsoft Windows Registry
	
	SYMPTOMS
	========
	
	When a Microsoft Exchange Client or Microsoft Outlook user changes the Windows
	NT or Windows 2000 password either by clicking "Change Password" in the "Enter
	Password" dialog box or on the Tools menu, clicking Options, on the Security
	tab, clicking "Change Settings", and then clicking Password, one of the
	following error messages is displayed:
	
	  The Windows NT Domain password could not be changed. A required action was
	  not successful due to an unspecified error.
	
	  The Windows NT password could not be changed. Please check the information
	  and try again.
	
	NOTE: The error messages begin with "The Windows 2000..." when you change a
	Windows 2000 password.
	
	CAUSE
	=====
	
	The client is not logged on to the domain that the password is changed in, or to
	a trusted domain. Therefore, the client cannot establish a remote procedure call
	(RPC) connection to the Local Security Authority (LSA) to change the password.
	
	The following clients have this problem:
	
	- Clients that use the NetWare Client software.
	
	For additional information about how NetWare Clients change passwords, click the
	article number below to view the article in the Microsoft Knowledge Base:
	
	  Q148420 XCLN: Can't Change Password on Novell Client
	
	- Clients that use Macintosh messaging clients.
	
	For additional information about how Macintosh messaging clients change
	passwords, click the article number below to view the article in the Microsoft
	Knowledge Base:
	
	  Q156182 XCLN: Changing Windows NT 4.0 Password in Microsoft Exchange
	
	- Clients that use Banyan Vines protocol.
	
	For additional information about Banyan Vines protocol, click the article number
	below to view the article in the Microsoft Knowledge Base:
	
	  Q140641 Updated Samsrv.dll Supports AppleTalk and Banyan Vines Clients
	
	- Clients that log on to an untrusted Windows NT domain or a workgroup.
	
	RESOLUTION
	==========
	
	WARNING: If you use Registry Editor incorrectly, you may cause serious problems
	that may require you to reinstall your operating system. Microsoft cannot
	guarantee that you can solve problems that result from using Registry Editor
	incorrectly. Use Registry Editor at your own risk.
	
	NOTE: Normally, registry entries are not case sensitive. However, these entries
	are case sensitive. When you add any of these new keys, be sure to match the
	case exactly.
	
	Add the following registry values to the PDC in a NT Domain or the PDC-Emulator
	in a Windows 2000 Domain:
	
	1. Start Registry Editor (Regedt32.exe).
	
	2. Under the HKEY_LOCAL_MACHINE subtree, go to the following subkey:
	
	  SYSTEM\CurrentControlSet\Control\LSA
	
	3. On the Edit menu, click Add Value.
	
	4. Add one of the following values, depending on which protocol is shared
	  between the clients and the PDC:
	
	  NetWareClientSupport
	
	  TCPIPClientSupport
	
	  VinesClientSupport
	
	  AppletalkClientSupport
	
	5. In the Data Type field, select REG_DWORD, and then click OK.
	
	6. In the DWORD editor, in the Data field, type "1" (without the quotation
	  marks).
	
	7. Click OK. The new value appears.
	
	8. You must restart the PDC for the changes to take effect.
	
	MORE INFORMATION
	================
	
	When an Outlook client changes a Windows NT or a Windows 2000 password, the
	client asks the Exchange Server computer for the name of the PDC in a NT 4.0
	domain or the PDC-Emulator in a Windows 2000 domain. The client then establishes
	an RPC connection with the LSA on the PDC or PDC-Emulator.
	
	To locate the server running the PDC-Emulator role use the NETDOM tool from the
	Windows Support tools on the Windows 2000 Server CD and execute the following
	command.
	
	  "NETDOM QUERY FSMO" (without the quotation marks)
	
	Note the server name listed next to the line labeled PDC Role will be the server
	to get the registry values added.
	
	The LSA, by default, has no endpoint mapped for TCP/IP, IPX/SPX, AppleTalk, or
	Banyan Vines. It does not have this problem with named pipes. Clients that log
	on to the same domain as the PDC have no problem making a named pipes connection
	and changing their passwords.
	
	This registry change mentioned in the "Resolution" section of this article should
	be made on the server running the PDC-Emulator role in a Windows 2000 Domain. If
	the Role of the PDC-Emulator moves to another Domain Controller in the Windows
	2000 Domain, the registry on the new Domain Controller will need to be updated
	with the registry change.
	
	
	Additional query words: 8.0 8.01 8.02 8.03 8.04 8.5 9.0
	
	======================================================================
	Keywords          :  
	Technology        : kbwin2000AdvServ kbwin2000AdvServSearch kbwin2000Serv kbwin2000ServSearch kbwin2000Search kbHWMAC kbOSMAC kbOutlookSearch kbOutlook2001 kbExchangeSearch kbExchange500 kbExchange400 kbExchangeClientSearch kbZNotKeyword kbOutlook2002 kbZNotKeyword2 kbOutlook2000Search kbOutlook2002Search kbOutlook97Search kbOutlook98Search kbOutlook2001Search kbWinAdvServSearch kbZNotKeyword3 kbOutlookMacSearch kbExchange500Mac kbExchange400Mac kbExchange400NT kbExchange500NT kbOutlook800Mac kbOutlook810Mac kbOutlook820Mac kbExchange400Win95 kbExchange500Win95
	Version           : :2000,4.0,5.0,8.0,8.1,8.2
	Issue type        : kbprb
	
	=============================================================================
	

{% endraw %}
