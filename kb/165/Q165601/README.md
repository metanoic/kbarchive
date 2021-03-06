---
layout: page
title: "Q165601: WD97: Macro Record Results In PlayBack Error Editing Objects"
permalink: /kb/165/Q165601/
---

## Q165601: WD97: Macro Record Results In PlayBack Error Editing Objects

{% raw %}

	Article: Q165601
	Product(s): Word 97 for Windows
	Version(s): WINDOWS:97
	Operating System(s): 
	Keyword(s): kbmacro kbdta kbdtacode word8 kbwordvba word97
	Last Modified: 13-MAY-2002
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Word 97 for Windows 
	-------------------------------------------------------------------------------
	
	
	SYMPTOMS
	========
	
	When you record a Visual Basic for Applications macro that locates an OLE object
	by clicking GoTo on the Edit menu and then edits the object by clicking Object
	on the Edit menu, the following error message may appear when you play back the
	recorded macro:
	
	  Run-time error '5941':
	  The requested member of the collection does not exist.
	
	CAUSE
	=====
	
	Using the GoTo command (on the Edit menu) does not select the object. However,
	Visual Basic for Applications records this action using the Selection property
	for the object instead of the ActiveDocument property. Because the object is not
	selected, it is not a member of the Selection Object.
	
	WORKAROUND
	==========
	
	Microsoft provides programming examples for illustration only, without warranty
	either expressed or implied, including, but not limited to, the implied
	warranties of merchantability and/or fitness for a particular purpose. This
	article assumes that you are familiar with the programming language being
	demonstrated and the tools used to create and debug procedures. Microsoft
	support professionals can help explain the functionality of a particular
	procedure, but they will not modify these examples to provide added
	functionality or construct procedures to meet your specific needs. If you have
	limited programming experience, you may want to contact a Microsoft Certified
	Partner or the Microsoft fee-based consulting line at (800) 936-5200. For more
	information about Microsoft Certified Partners, please visit the following
	Microsoft Web site:
	
	  http://www.microsoft.com/partner/referral/
	
	For more information about the support options that are available and about how
	to contact Microsoft, visit the following Microsoft Web site:
	
	  http://support.microsoft.com/default.aspx?scid=fh;EN-US;CNTACTMS
	
	To work around this problem, edit the macro and change the Selection property to
	the ActiveDocument property. For example, change this code:
	
	     Selection.InlineShapes(1).OLEFormat.DoVerb _
	     VerbIndex:=wdOLEVerbPrimary
	
	to this code:
	
	     ActiveDocument.InlineShapes(1).OLEFormat.DoVerb _
	     VerbIndex:=wdOLEVerbPrimary
	
	For more information about how to edit a macro, click the Office Assistant while
	in the Visual Basic Editor, type "edit a macro" (without the quotation marks)
	click Search, and then click to view "Edit a macro."
	
	NOTE: If the Assistant is hidden, click the Office Assistant button on the
	Standard toolbar. If the Assistant is not able to answer your query, please see
	the following article in the Microsoft Knowledge Base:
	
	  Q176476 OFF: Office Assistant Not Answering Visual Basic Questions
	
	STATUS
	======
	
	Microsoft has confirmed this to be a problem in the Microsoft products listed at
	the beginning of this article.
	
	MORE INFORMATION
	================
	
	For additional information, please see the following article in the Microsoft
	Knowledge Base:
	
	  Q173707 OFF97: How to Run Sample Code from Knowledge Base Articles
	
	
	REFERENCES
	==========
	
	For more information about getting help with Visual Basic for Applications,
	please see the following article in the Microsoft Knowledge Base:
	
	  Q163435 VBA: Programming Resources for Visual Basic for Applications
	
	Additional query words: wordcon vb vba vbe
	
	======================================================================
	Keywords          : kbmacro kbdta kbdtacode word8 kbwordvba word97 
	Technology        : kbWordSearch kbWord97 kbWord97Search kbZNotKeyword2
	Version           : WINDOWS:97
	Hardware          : x86
	Issue type        : kbbug
	Solution Type     : kbnofix
	
	=============================================================================
	

{% endraw %}
