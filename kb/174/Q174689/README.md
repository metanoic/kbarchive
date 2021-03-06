---
layout: page
title: "Q174689: HOWTO: Set a Primary Key to Updateable in a View"
permalink: /kb/174/Q174689/
---

## Q174689: HOWTO: Set a Primary Key to Updateable in a View

{% raw %}

	Article: Q174689
	Product(s): Microsoft FoxPro
	Version(s): MACINTOSH:3.0b; WINDOWS:2.5,5.0,5.0a,6.0
	Operating System(s): 
	Keyword(s): kbcode kbDatabase kbHWMAC kbvfp300 kbvfp500 kbvfp600 KbDBFDBC kbMDAC250
	Last Modified: 22-FEB-2000
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Visual FoxPro for Windows, versions 5.0, 5.0a, 6.0 
	- Microsoft Visual FoxPro for Macintosh, version 3.0b 
	- Microsoft Data Access Components version 2.5 
	-------------------------------------------------------------------------------
	
	SUMMARY
	=======
	
	By default, when creating a view on a table, any field with a primary key index
	is not marked as updateable. This article illustrates how you can mark the
	primary key as updateable through the View Designer, and programmatically.
	
	MORE INFORMATION
	================
	
	View Designer
	-------------
	
	To mark the primary key as updateable through the View Designer interface, use
	the following steps:
	
	1. Open the view in the View Designer.
	
	2. Click the Update Criteria tab.
	
	3. Click the Update column beside the primary key field.
	
	  NOTE: The Update column has a column header that looks like a pencil. If you
	  do not select the Update column and you attempt to INSERT a new record, you
	  may receive one of the following errors:
	
	  Connectivity error: [Microsoft][ODBC Visual FoxPro Driver Field
	  <fieldname> does not accept null values.
	
	  -or-
	
	  Mandatory not null field - missing or null during insert.
	
	Programmatically
	----------------
	
	To mark the primary key as updateable programmatically, use the following steps:
	
	1. Open the Tastrade database in the VFP\Samples\Tastrade\Data folder in Visual
	  FoxPro 5.0, or the home(2)+"Tastrade\Data" folder in Visual FoxPro 6.0.
	
	2. Run the following program to create a new SQL view based on the Customer
	  table.
	
	        ***********RunFirst.prg***********
	        CREATE SQL VIEW MYTEST AS SELECT * FROM CUSTOMER
	        DBSETPROP("MYTEST","VIEW","SENDUPDATES",.T.)
	        ***********End RunFirst.prg*************
	
	3. Modify the view in the View Designer and note that the primary key is not
	  marked for updates.
	
	4. Create a program called MarkPrimary and place the following code in it:
	
	        ************MarkPrimary.prg****************
	        PARAMETERS ViewName
	
	        x=ALIAS()
	        USE IN 0 &viewname
	        PrimKeys = CURSORGETPROP('KeyFieldList',viewname)
	        i=1
	        remField=PrimKeys
	        DO WHILE i <> 0
	           nextcomma=AT(remField,",")
	           IF nextcomma=0 and len(remfield)=0 THEN
	              i=0
	              EXIT
	           ELSE
	              IF nextcomma=0 and LEN(remfield)<>0 then
	                 tmpfield=remfield
	                 y= DBSETPROP(ViewName + "." + ;
	                 tmpField,'Field','UPDATABLE',.T.)
	                 i=0
	                 EXIT
	              ELSE
	                 tmpField=SUBSTR(remField,i,NextComma -1)
	                 remfield=SUBSTR(remfield,nextcomma + 1)
	                 i=nextcomma
	                 y= DBSETPROP(ViewName + "." + ;
	                 tmpField,'Field','UPDATABLE',.T.)
	              ENDIF
	           ENDIF
	        ENDDO
	
	        SELECT  (viewname)
	        USE
	        IF NOT EMPTY(x) THEN
	           SELECT  (x)
	        ENDIF
	        **************End MarkPrimary.prg*******************
	
	5. Run the MarkPrimary.prg code by typing the following into the Command
	  window:
	
	        DO MARKPRIMARY WITH "MYTEST"
	
	6. Modify the view MyTest in the View Designer and notice that the primary key
	  field is now marked for updates.
	
	Additional query words:
	
	======================================================================
	Keywords          : kbcode kbDatabase kbHWMAC kbvfp300 kbvfp500 kbvfp600 KbDBFDBC kbMDAC250 
	Technology        : kbHWMAC kbOSMAC kbVFPsearch kbAudDeveloper kbMDACSearch kbMDAC250 kbVFP300bMac kbVFP500 kbVFP600 kbVFP500a
	Version           : MACINTOSH:3.0b; WINDOWS:2.5,5.0,5.0a,6.0
	Issue type        : kbhowto
	
	=============================================================================
	

{% endraw %}
