---
layout: page
title: "Q196436: WD97: &quot;Blue Background, White Text&quot; Option Makes Text Disappear"
permalink: /kb/196/Q196436/
---

## Q196436: WD97: &quot;Blue Background, White Text&quot; Option Makes Text Disappear

{% raw %}

	Article: Q196436
	Product(s): Word 97 for Windows
	Version(s): WINDOWS:97
	Operating System(s): 
	Keyword(s): word97
	Last Modified: 14-NOV-2000
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Word 97 for Windows 
	-------------------------------------------------------------------------------
	
	
	SYMPTOMS
	========
	
	Black text on a white background may become invisible when the "Blue background,
	white text" option is selected. For example, this problem may occur when you
	have text typed in a text box.
	
	The text is visible in print preview but not in normal or page layout views;
	however, the text prints correctly, as shown in print preview.
	
	CAUSE
	=====
	
	By default, the background shading (fill color) of text boxes is white. When
	"Blue background, white text" is selected, text contained in a text box is also
	displayed as white; therefore, the text is not visible against the white fill
	color of the text box.
	
	WORKAROUND
	==========
	
	To work around this problem, use any of the following methods.
	
	Method 1: Set the Text Box Fill Color to No Fill
	------------------------------------------------
	
	1. Select the text box.
	
	2. On the Format menu, click Text Box.
	
	3. On the Colors And Lines tab, under Fill, change the Color box to No Fill, and
	  then click OK.
	
	Method 2: Clear the "Blue Background, White Text" Option
	--------------------------------------------------------
	
	1. On the Tools menu, click Options.
	
	2. On the General tab, click to clear the "Blue background, white text" check
	  box.
	
	3. Click OK.
	
	Method 3: Change the Font Color to Black
	----------------------------------------
	
	To use a font color other than white, follow these steps:
	
	1. Select the text that is not visible in "Blue background, white text" mode.
	
	2. On the Format menu, click Font.
	
	3. On the Color list, select Black (instead of Auto).
	
	MORE INFORMATION
	================
	
	The "Blue background, white text" option changes the background color of the
	document to blue and changes the text color to white. Some users find this
	setting to be easier to read than the default setting (black text on a white
	background).
	
	In addition, if you choose the General tab in the Options dialog box on the Tools
	menu and select the "Blue background, white text" option, you may have
	difficulty seeing the green underlining for items flagged as grammar issues.
	
	Currently there is no option for changing the color of underlined grammar flagged
	text in Word 97.
	
	REFERENCES
	==========
	
	For more information about the blue background with white text feature, please
	see the following articles in the Microsoft Knowledge Base:
	
	  Q114995 Preview Page Contains No Lines in File Page Setup Dialog Box
	
	  Q170944 WD97: Page Border Art Has a White Background
	
	  Q127093 Word Uses Orange Highlight Color When Blue/White Selected
	
	  Q113700 Changing the Background Color of the Document Window
	
	Additional query words: green underline underlined wavy
	
	======================================================================
	Keywords          : word97 
	Technology        : kbWordSearch kbWord97 kbWord97Search kbZNotKeyword2
	Version           : WINDOWS:97
	Issue type        : kbprb
	
	=============================================================================
	

{% endraw %}
