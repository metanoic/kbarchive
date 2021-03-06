---
layout: page
title: "Q76776: README.TXT: Running Specific Non-Windows Applications"
permalink: /kb/076/Q76776/
---

## Q76776: README.TXT: Running Specific Non-Windows Applications

{% raw %}

	Article: Q76776
	Product(s): Microsoft Windows 3.x Retail Product
	Version(s): 1.0
	Operating System(s): 
	Keyword(s): 
	Last Modified: 10-OCT-1999
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Windows with Multimedia Extensions, version 1.0 
	-------------------------------------------------------------------------------
	
	SUMMARY
	=======
	
	The following information is contained in the Windows with Multimedia Extensions
	version 1.0 README.TXT file. The Setup program copies this file to the Windows
	with Multimedia Extensions directory.
	
	This information does not apply to later versions of Windows.
	
	RUNNING SPECIFIC NON-WINDOWS APPLICATIONS
	=========================================
	
	This section describes some problems you might have running
	non-Windows applications with Windows 3.0.
	
	Microsoft Flight Simulator
	--------------------------
	
	Microsoft Flight Simulator cannot be run as a background application.
	When you are running Windows in standard or real modes, do not switch
	from Flight Simulator (ALT+TAB or ALT+ESC) to any other application.
	
	Using MultiSoft PC-Kwik Disk Accelerator
	----------------------------------------
	
	If you use PC-Kwik with Windows running in 386 enhanced mode, make
	sure the version is 3.55 or later and that you use PC-Kwik in extended
	memory, not expanded memory.
	
	If you need to upgrade your version of PC-Kwik, call MultiSoft at
	1-800-888-KWIK in the United States. Outside the U.S., call
	1-503-644-5644.
	
	Professional Oracle
	-------------------
	
	You can run Oracle only in real mode, and without the HIMEM extended
	memory driver loaded.
	
	QModem
	------
	
	If you have problems running QModem with Windows, create a program
	information file (PIF) for QModem that specifies a limit of 0 for EMS
	memory. Specifying 0 disables EMS for QModem, freeing that memory for
	use by Windows.
	
	Borland Reflex
	--------------
	
	If you have performance problems running Borland Reflex with Windows
	in 386 enhanced mode, include the following line in the [386Enh]
	section of your SYSTEM.INI file:
	
	  VirtualHDIrq=FALSE
	
	Microsoft Word
	--------------
	
	You might have problems using ALT+TAB with Microsoft Word 5.0 and also
	using ALT+SPACEBAR to transfer data into Microsoft Word 5.0 from the
	Windows 3.0 Clipboard. If so, contact Microsoft Customer Service for
	an updated version of Microsoft Word 5.0. The updated version contains
	a keyboard driver that lets you use ALT+TAB and ALT+SPACEBAR.
	
	Lotus 1-2-3
	-----------
	
	Some versions of Lotus 1-2-3 require you to insert a floppy disk that
	contains a software "key". When running with Windows in 386 enhanced
	mode, a "key" version of 1-2-3 might display an error message telling
	you that the disk drive is not ready. Or, Windows might terminate
	1-2-3 and display a message telling you that the application has
	violated system integrity.  You can prevent these problems by doing
	one of the following:
	
	- Make sure no other non-Windows applications are running when
	  you start 1-2-3.
	
	  -or-
	
	- Edit the PIF for 1-2-3, and check the "Execution: Exclusive" box.
	
	Additional query words: MMWIN kbmm 1.00 readme
	
	======================================================================
	Keywords          :  
	Technology        : kbWinMultiXSearch kbWinMultiX100
	Version           : :1.0
	
	=============================================================================
	

{% endraw %}
