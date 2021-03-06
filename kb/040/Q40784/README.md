---
layout: page
title: "Q40784: CodeView Does Not Work with Grouped Code Segments"
permalink: /kb/040/Q40784/
---

## Q40784: CodeView Does Not Work with Grouped Code Segments

{% raw %}

	Article: Q40784
	Product(s): Microsoft Programming Utilities
	Version(s): 2.2,3.0,3.11,3.12,3.14,3.5,4.0,4.01,4.05,4.1
	Operating System(s): 
	Keyword(s): kb16bitonly
	Last Modified: 26-JUN-2001
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft CodeView for MS-DOS, versions 2.2, 3.0, 3.11, 3.14, 4.0, 4.01, 4.05, 4.1 
	- Microsoft CodeView for OS/2, versions 2.2, 3.0, 3.11, 3.12, 3.5 
	-------------------------------------------------------------------------------
	
	Using the Microsoft Macro Assembler (MASM), it is possible to
	associate various segments into a group; DGROUP is an example of this
	technique. Grouped data or stack segments do not affect CodeView but
	CodeView does not recognize grouped code segments. The program will
	run correctly under CodeView but none of the CodeView functions will
	be available on the second and subsequent segments in the code group.
	
	The sample code below illustrates this behavior. Once the program
	executes into the _TEXTB segment, all CodeView functionality is lost.
	You cannot set any breakpoints or single step through the _TEXTB code.
	Any attempt to single trace into _TEXTB will result in CodeView
	running all the code in _TEXTB as if you had specified a go or a step
	
	Sample Code
	-----------
	
	  ; Assembler options needed: /Zi
	
	          DOSSEG
	  _TEXT   GROUP   _TEXTA, _TEXTB         ; Code group _TEXT
	
	  _DATA   SEGMENT WORD PUBLIC 'DATA'
	  msg     DB      "Hello, world.", 13, 10, "$"
	  _DATA   ENDS
	
	  _TEXTA  SEGMENT WORD PUBLIC 'CODE'     ; First code segment - this
	          ASSUME  cs:_TEXT,ds:_DATA      ;  code may be traced as
	  start:  mov     ax, _DATA              ;  expected.
	          mov     ds, ax
	          call    FAR PTR SayHi
	          mov     ax, 4C00h
	          int     21h
	  _TEXTA  ENDS
	
	  _TEXTB  SEGMENT WORD PUBLIC 'CODE'     ; You cannot trace through
	  SayHi   PROC                           ;  this code.
	          mov     ah, 9h
	          mov     dx, OFFSET msg
	          int     21h
	          ret
	  SayHi   ENDP
	  _TEXTB  ENDS
	
	          END     start
	
	Additional query words: kbinf 2.20 3.00 3.50 4.10
	
	======================================================================
	Keywords          : kb16bitonly 
	Technology        : kbAudDeveloper kbCodeView kbZNotKeyword3 kbCodeView220DOS kbCodeView300DOS kbCodeView311DOS kbCodeView314DOS kbCodeView400DOS kbCodeView401DOS kbCodeView405DOS kbCodeView410DOS kbCodeView220OS2 kbCodeView300OS2 kbCodeView311OS2 kbCodeView312OS2 kbCodeView350OS2
	Version           : :2.2,3.0,3.11,3.12,3.14,3.5,4.0,4.01,4.05,4.1
	
	=============================================================================
	

{% endraw %}
