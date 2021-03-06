---
layout: page
title: "Q111531: FORMAT /S and SYS Copy Invalid System File with 4DOS or NDOS"
permalink: /kb/111/Q111531/
---

## Q111531: FORMAT /S and SYS Copy Invalid System File with 4DOS or NDOS

{% raw %}

	Article: Q111531
	Product(s): Microsoft Disk Operating System
	Version(s): MS-DOS:5.0,5.0a,6.0,6.2,6.21,6.22
	Operating System(s): 
	Keyword(s): 
	Last Modified: 19-NOV-1999
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft MS-DOS operating system versions 5.0, 5.0a, 6.0, 6.2, 6.21, 6.22 
	-------------------------------------------------------------------------------
	
	SYMPTOMS
	========
	
	After you use the MS-DOS FORMAT /S or SYS command to create a system disk, you
	receive the following error message when you try to use that disk to start your
	system:
	
	  Bad or Missing Command Interpreter
	  Enter correct name of Command Interpreter (e.g., C:\COMMAND.COM)
	
	CAUSE
	=====
	
	This error occurs if JP Software's 4DOS.COM, Symantec's NDOS.COM, or another
	third-party replacement for MS-DOS COMMAND.COM was loaded as the command
	interpreter at the time you created the system disk. The FORMAT /S and SYS
	commands copy the file currently specified in the COMSPEC environment (for
	example, NDOS.COM or 4DOS.COM) to the system disk being created as
	"COMMAND.COM."
	
	RESOLUTION
	==========
	
	To correct this problem, replace the third-party shell, NDOS.COM or 4DOS.COM,
	with MS-DOS COMMAND.COM, then transfer the system files to the disk again using
	the MS-DOS FORMAT /S or SYS command.
	
	MORE INFORMATION
	================
	
	The products NDOS and 4DOS are manufactured by vendors independent of Microsoft;
	we make no warranty, implied or otherwise, regarding these products' performance
	or reliability.
	
	Additional query words: 6.22 6.20 6.00 5.00 4DOS NDOS
	
	======================================================================
	Keywords          :  
	Technology        : kbMSDOSSearch kbMSDOS621 kbMSDOS622 kbMSDOS620 kbMSDOS600 kbMSDOS500 kbMSDOS500a
	Version           : MS-DOS:5.0,5.0a,6.0,6.2,6.21,6.22
	
	=============================================================================
	

{% endraw %}
