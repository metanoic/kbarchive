---
layout: page
title: "Q189489: FIX: Binary Compatibility Broken When Adding Events"
permalink: /kb/189/Q189489/
---

## Q189489: FIX: Binary Compatibility Broken When Adding Events

{% raw %}

	Article: Q189489
	Product(s): Microsoft Visual Basic for Windows
	Version(s): WINDOWS:5.0
	Operating System(s): 
	Keyword(s): kbGrpDSVB
	Last Modified: 11-JAN-2001
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Visual Basic Professional Edition for Windows, version 5.0 
	- Microsoft Visual Basic Enterprise Edition for Windows, version 5.0 
	-------------------------------------------------------------------------------
	
	SYMPTOMS
	========
	
	Adding Events to an ActiveX EXE Object whose instancing property is set to
	"PublicNotCreatable" may result in the following Binary Compatibility error:
	
	  The <Class Name> Class Implemented An Interface In The
	  Version-Compatible Component, But Not In The Current Project.
	
	STATUS
	======
	
	Microsoft has confirmed this to be a bug in the Microsoft products listed at the
	beginning of this article. This bug has been fixed in Visual Basic 6.0
	
	MORE INFORMATION
	================
	
	Steps to Reproduce Behavior
	---------------------------
	
	1. Create a new ActiveX EXE project in Visual Basic 5.0. Class1 is created by
	  default.
	
	2. Set the Class1 instancing property to "2-PublicNotCreatable."
	
	3. Add a new Class Module (Class2) to the project.
	
	4. Select Make Project1.exe from the File menu.
	
	5. Select Project1 Properties from the Project menu, then select the Component
	  tab.
	
	6. Select the Binary Compatibility option button under the Version Compatibility
	  section. Project1.exe should automatically be shown in the textbox.
	
	7. In the Class1 code window, add the following statement:
	
	        Public Event MyEvent()
	
	8. Repeat step 6. Select "Yes" to overwrite the older file when asked. The
	  following message will appear:
	
	  The Class1 Class Implemented An Interface In The Version-Compatible
	  Component, But Not In The Current Project.
	
	Additional query words: kbDSupport kbActiveX kbVBp500bug kbVBp600fix kbVBp kbdss
	
	======================================================================
	Keywords          : kbGrpDSVB 
	Technology        : kbVBSearch kbAudDeveloper kbZNotKeyword6 kbZNotKeyword2 kbVB500Search kbVBA500 kbVB500
	Version           : WINDOWS:5.0
	Issue type        : kbbug
	Solution Type     : kbfix
	
	=============================================================================
	

{% endraw %}
