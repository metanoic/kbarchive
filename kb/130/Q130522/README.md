---
layout: page
title: "Q130522: Internal Memory Management in Visual FoxPro"
permalink: /kb/130/Q130522/
---

## Q130522: Internal Memory Management in Visual FoxPro

{% raw %}

	Article: Q130522
	Product(s): Microsoft FoxPro
	Version(s): 3.00
	Operating System(s): 
	Keyword(s): kbenv
	Last Modified: 17-AUG-1999
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Visual FoxPro for Windows, version 3.0 
	-------------------------------------------------------------------------------
	
	SUMMARY
	=======
	
	Visual FoxPro handles memory management differently from previous versions of
	FoxPro. With FoxPro version 2.x, FoxPro had to pre-allocate one or more blocks
	of memory at startup. This is demonstrated by using MVCOUNT and MEMLIMIT. Visual
	FoxPro uses a more dynamic approach to memory management.
	
	MORE INFORMATION
	================
	
	In Visual FoxPro, a small footprint is allocated and the reserved memory pool is
	dynamically increased as needed. When free contiguous space in the currently
	allocated blocks used by Visual FoxPro becomes low, Visual FoxPro will try to
	compress the memory block. If Visual FoxPro still needs more memory after
	compression, it requests another memory block from the operating system.
	
	The requested block size is large, so Visual FoxPro doesn't have to send requests
	to the operating system often.
	
	Along the same lines, Visual FoxPro doesn't release memory from the pool until
	the operating system requests it back. This is done because memory requested by
	Visual FoxPro is assumed to be needed again. It requires a lot of time to
	request memory from the operating system, so Visual FoxPro holds on to whatever
	it requests.
	
	Memory Pools
	------------
	
	When Visual FoxPro starts, it creates two memory pools (FOX USER and FOX
	BUFFERS). The FOX USER area stores memory variables, and FOX BUFFERS stores
	strings that are embedded in the product as well as any structures that are
	related to files that are open. Visual FoxPro pulls memory from three existing
	Windows resources - OLE, USER, and GDI resources.
	
	Example Showing How Memory Pools Are Used
	-----------------------------------------
	
	When a user opens a form owning a private DataSession and that form is
	instantiated, Visual FoxPro uses memory from the FOX USER pool to store
	information about the session and properties of the form. The FOX BUFFERS pool
	is used to cache parts of the tables that are open in the DataSession.
	
	There is no Visual FoxPro command that forces the FoxPro memory manager to
	release the reserved memory blocks. The commands CLEAR ALL, RELEASE ALL, CLOSE
	ALL have no effect.
	
	Additional query words: VFoxWin
	
	======================================================================
	Keywords          : kbenv 
	Technology        : kbVFPsearch kbAudDeveloper kbVFP300
	Version           : 3.00
	
	=============================================================================
	

{% endraw %}
