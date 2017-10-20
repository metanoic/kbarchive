---
layout: page
title: "Q61609: Specific Status of Process ID and CWAIT"
permalink: /kb/061/Q61609/
---

## Q61609: Specific Status of Process ID and CWAIT

	Article: Q61609
	Product(s): See article
	Version(s): 5.10 6.00
	Operating System(s): OS/2
	Keyword(s): ENDUSER | | mspl13_c
	Last Modified: 29-MAY-1990
	
	Question:
	
	I spawned a child process under OS/2 using the following code:
	
	     pid = spawnve(P_NOWAITO,...parameter list...)
	          if (pid != -1)
	               status = cwait(&termstat, pid, WAIT_CHILD);
	
	Why does CWAIT always return status==-1 and with errno set to ECHILD
	even though the child runs successfully?
	
	Response:
	
	If not NULL, <termstat> points to a buffer that will contain a
	termination-status word and return code for the child process. The
	status word indicates whether the child terminated normally by calling
	the OS/2 DosExit function.
	
	When errno is set to ECHILD it is defined as follows:
	
	   ECHILD   No child process.
	
	            A wait was attempted by a thread that has no child
	            processes, or whose child process had the no-wait option
	            specified.
	
	In this case, the garbage value for TERMSTAT was generated by using
	P_NOWAITO rather than P_NOWAIT. In other words, the original spawn()
	call made the cwait() call fail. We document P_NOWAIT and P_NOWAITO as
	follows:
	
	   P_NOWAIT Continues to execute parent process concurrently with child
	            process.
	
	   P_NOWAITO Continues to execute parent process and ignores wait and
	             cwait calls against child process.