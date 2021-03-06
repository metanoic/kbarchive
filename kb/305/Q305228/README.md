---
layout: page
title: "Q305228: &quot;STOP 0xA&quot; Occurs After Applying Windows NT 4.0 SRP"
permalink: /kb/305/Q305228/
---

## Q305228: &quot;STOP 0xA&quot; Occurs After Applying Windows NT 4.0 SRP

{% raw %}

	Article: Q305228
	Product(s): Microsoft Windows NT
	Version(s): 4.0 SP6a
	Operating System(s): 
	Keyword(s): kb3rdparty kbenv kberrmsg
	Last Modified: 11-OCT-2001
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Windows NT Server version 4.0 SP6a 
	- Microsoft Windows NT Server, Enterprise Edition version 4.0 SP6a 
	- Microsoft Windows NT Workstation version 4.0 SP6a 
	-------------------------------------------------------------------------------
	
	SYMPTOMS
	========
	
	After you apply the Windows NT 4.0 Security Rollup Package (SRP) and restart a
	computer that has one of the following Compaq Smart Array controllers, you may
	receive an error message on a blue screen:
	
	- Compaq SMART Array controller
	- Compaq SMART-2/E Array controller
	- Compaq SMART-2/P Array controller
	- Compaq SMART-2DH Array controller
	- Compaq SMART-2SL Array controller
	- Compaq Smart Array 3200 controller
	- Compaq Smart Array 3100ES controller
	- Compaq Smart Array 221 controller
	
	This is the error message that you may receive:
	
	  STOP 0x0000000A (0xfcc35000, 0xa, 0x00000001, 0x801e092a)
	  IRQL_NOT_LESS_OR_EQUAL
	
	In this error message, the memory that is referenced is 0xfcc35000. The IRQL is
	0xa (IRQ 10). Value 0 is a read operation; 1 is a write operation. The address
	that referenced memory is 0x801e092a.
	
	CAUSE
	=====
	
	The Windows NT 4.0 SRP exposes an issue with versions earlier than 4.24.0.0 of
	the Compaq Array Controller device driver (Cpqarray.sys) that is available from
	any of the following sources:
	
	- Compaq Web site: Compaq Server Support (SSD) for Microsoft Windows NT 4.0
	- Compaq SmartStart and Support Software CD-ROM
	- Compaq SmartStart for Servers
	
	For additional information about these packages, visit the Compaq Web site:
	
	  http://www.compaq.com/
	
	RESOLUTION
	==========
	
	To resolve this issue, obtain the updated version of the Cpqarray.sys driver
	from the following Compaq Web site:
	
	  ftp://ftp.compaq.com/pub/products/servers/supportsoftware/cp001001-001500/cp001095.exe
	
	The third-party contact information included in this article is provided to help
	you find the technical support you need. This contact information is subject to
	change without notice. Microsoft in no way guarantees the accuracy of this
	third-party contact information.
	
	To prevent this problem from occurring, install the updated Cpqarray.sys driver
	before you install the SRP.
	
	WORKAROUND
	==========
	
	If you cannot obtain the updated Cpqarray.sys driver that is described earlier
	in this article, you can work around this issue by replacing the existing
	Cpqarray.sys file with the version from Microsoft Windows NT 4.0 Service Pack 6a
	(SP6a):
	
	1. If the partition uses the NTFS file system, install Windows NT in a different
	  folder so that the files in the partition are accessible.
	
	  If the partition uses the FAT file system, start the computer by using an
	  MS-DOS boot disk, and then skip to step 3.
	
	2. Boot the computer to the new installation of Windows NT.
	
	3. Copy the Cpqarray.sys file from Windows NT 4.0 SP6a to the original Windows
	  NT 4.0 folder (%SystemRoot%\System32\Drivers).
	
	4. You may also use the Recovery Console from Windows 2000 to rename the
	  offending driver and replace it with CPQARRAY.SYS from SP6a.
	
	
	As an alternative, you can use the Scsiport.sys file from Windows NT 4.0 SP6a to
	start your computer. This causes several fixes that are included with the
	Windows NT 4.0 Security Rollup Package to be removed. The advantage to using
	this method is that any additional functionality that is included in the Compaq
	version of the Cpqarray.sys driver is available. To replace the Scsiport.sys
	file, use the preceding steps, but copy the Scsiport.sys file instead of the
	Cpqarray.sys file.
	
	MORE INFORMATION
	================
	
	For additional information about the Windows NT 4.0 Security Rollup Package,
	click the article number below to view the article in the Microsoft Knowledge
	Base:
	
	  Q299444 Post-Windows NT 4.0 Service Pack 6a Security Rollup Package (SRP)
	
	
	
	Additional query words: srp windows update stop 0x0000000a sbs critical updates compaq
	
	======================================================================
	Keywords          : kb3rdparty kbenv kberrmsg 
	Technology        : kbWinNTsearch kbWinNTWsearch kbWinNTW400search kbWinNT400search kbWinNTSsearch kbWinNTSEntSearch kbWinNTS400sp6 kbWinNTS400search kbWinNTSEnt400SP6a kbWinNTW400SP6a
	Version           : :4.0 SP6a
	Issue type        : kbprb
	
	=============================================================================
	

{% endraw %}
