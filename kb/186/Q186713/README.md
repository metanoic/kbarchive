---
layout: page
title: "Q186713: Event IDs 1010, 1008, 1011, and 4005 with CIM and Perflib"
permalink: /kb/186/Q186713/
---

## Q186713: Event IDs 1010, 1008, 1011, and 4005 with CIM and Perflib

{% raw %}

	Article: Q186713
	Product(s): Microsoft SNA Server
	Version(s): WINDOWS:3.0,3.0 SP1,3.0 SP2,3.0 SP3,4.0
	Operating System(s): 
	Keyword(s): 
	Last Modified: 17-SEP-1999
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft SNA Server, versions 3.0, 3.0 SP1, 3.0 SP2, 3.0 SP3, 4.0 
	-------------------------------------------------------------------------------
	
	SYMPTOMS
	========
	
	The Windows NT Event Viewer Application log may generate Event ID 1010 logs
	every two to three seconds. The event description is as follows:
	
	  Event ID:  1010
	  Source:    Perflib
	  Description:
	  The Collect Procedure for the "SnaServr" service in DLL
	  "C:\SNA\system\snaperf.dll" generated an  exception or returned
	  an invalid status. Performance data returned by counter DLL will be not
	  be returned in Perf Data Block. Exception or status code returned is
	  DWORD 0.
	
	Other related events descriptions that may follow are:
	
	  Event ID:  1008
	  Source:    Perflib
	  Description:
	  The Open Procedure for service "Tcpip" in DLL "Perfctrs.dll" failed.
	  Performance data for this service will not be available. Status code
	  returned is DWORD 0.
	
	  Event ID:  1011
	  Source:    Perflib
	  Description:
	  The library file "tapiperf.dll" specified for the "TapiSrv" service
	  could not  be opened. Performance data for this service will not be
	  available.  Status code is data DWORD 0.
	
	  Event ID:  4005
	  Source:    perfctrs
	  Description:
	  Load of INETMIB1.DLL failed. Make sure the DLL file is in the PATH.
	  WIN32 Error number is returned in the data.
	
	CAUSE
	=====
	
	It has been confirmed that versions prior to 3.5 of Compaq's Insight Manager
	(CIM) conflict with Performance Counters causing these errors to occur.
	
	WORKAROUND
	==========
	
	To work around this problem, perform one of the following:
	
	- Disable Compaq's Insight Manager Agent from the Control Panel Services tool.
	
	  -or-
	
	- Install Compaq's Insight Manager version 3.5 or greater from their Support
	  Software Diskette (SSD).
	
	MORE INFORMATION
	================
	
	All the application event logs mentioned above are related to a conflict between
	CIM and Performance Monitor Counters used by either Windows NT services or
	applications installed, such as SNA Server, TCP/IP, TAPI (Telephony API) and the
	Simple Network Management Protocol (SNMP).
	
	Insight Manager is a third-party product manufactured by Compaq Corporation, a
	vendor independent of Microsoft; Microsoft makes no warranty, implied or
	otherwise, regarding this product's performance or reliability.
	
	Additional query words:
	
	======================================================================
	Keywords          :  
	Technology        : kbAudDeveloper kbSNAServSearch kbSNAServ300 kbSNAServ400 kbSNAServ300SP3 kbSNAServ300SP1 kbSNAServ300SP2
	Version           : WINDOWS:3.0,3.0 SP1,3.0 SP2,3.0 SP3,4.0
	Issue type        : kbprb
	
	=============================================================================
	

{% endraw %}
