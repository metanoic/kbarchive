---
layout: page
title: "Q193943: HOWTO: Use GetDeviceCaps to Determine Margins on a Page"
permalink: /kb/193/Q193943/
---

## Q193943: HOWTO: Use GetDeviceCaps to Determine Margins on a Page

{% raw %}

	Article: Q193943
	Product(s): Microsoft Visual Basic for Windows
	Version(s): 4.0,5.0,6.0
	Operating System(s): 
	Keyword(s): kbprint kbAPI kbPrinting kbVBp kbVBp400 kbVBp500 kbVBp600 kbGrpDSVB
	Last Modified: 03-JAN-2002
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Visual Basic Standard Edition, 32-bit, for Windows, version 4.0 
	- Microsoft Visual Basic Professional Edition, 32-bit, for Windows, version 4.0 
	- Microsoft Visual Basic Enterprise Edition, 32-bit, for Windows, version 4.0 
	- Microsoft Visual Basic Learning Edition for Windows, versions 5.0, 6.0 
	- Microsoft Visual Basic Professional Edition for Windows, versions 5.0, 6.0 
	- Microsoft Visual Basic Enterprise Edition for Windows, versions 5.0, 6.0 
	-------------------------------------------------------------------------------
	
	SUMMARY
	=======
	
	The Visual Basic Printer object only exposes the physical size and printable
	area of the paper you are printing on and does not give you access to the actual
	margins or unprintable areas. You can retrieve this information, however, by
	using the Win32 API function, GetDeviceCaps. This article demonstrates how to
	retrieve and use this information.
	
	MORE INFORMATION
	================
	
	GetDeviceCaps only takes two arguments. The first is a handle to the Device
	Context, "DC", of the device you want to query. In the example below, this is
	always the current printer. The second argument is a Long value that specifies
	the item to return. The following example includes only the definitions for the
	constants actually used in the demonstration code. In general, the units of the
	return value vary, but for the items used here, the unit of measurement is
	always pixels.
	
	In the sample below, Command1 contains code that calls the GetDeviceCaps API
	multiple times to retrieve various bits of printer information, which are then
	displayed all at once at the end of the routine. The information retrieved
	includes all of the default margins and describes the printable area of the
	page.
	
	The code for Command2 retrieves and uses the printer information to determine the
	lowest printing position on the page, and uses this to print a centered page
	footer that includes a page number. A page header, including the current date,
	right-justified, is printer at the top of each page. In addition, a report
	header prints at the top of the first page only. The sample further demonstrates
	setting custom margins within the printable area using the technique of checking
	the current X or Y position against a limit imposed in the code. You can easily
	modify this to allow the user to choose these margins and even the text for the
	footers or headers.
	
	The printable area of the page always starts at position 0,0 (Printer.CurrentX =
	0 and Printer.CurrentY = 0). By setting these values you can get to any point on
	the page. The PrintHeader procedure prints some text in italics, and other text
	normally, on the same line. It does this by changing the CurrentX and CurrentY
	values to return to a new position on line that was previously printed.
	
	NOTE: You can also mix font attributes by ending a print statement with a ";"
	semicolon. This retains the last print position without starting a new line at
	CurrentX = 0, which is the default behavior. In this way, you can print some
	text, change font attributes (bold, italic, and so on), then print more text
	starting right where you left off.
	
	Step-by-Step Example
	--------------------
	
	1. Start a new project in Visual Basic. Form1 is created by default.
	
	2. Add two CommandButtons to the Form and paste the following code into the
	  Form's module:
	
	        Option Explicit
	
	        Private Declare Function GetDeviceCaps Lib "gdi32" _
	         (ByVal hdc As Long, ByVal nIndex As Long) As Long
	
	        ' Constants for nIndex argument of GetDeviceCaps
	        Private Const HORZRES = 8
	        Private Const VERTRES = 10
	        Private Const LOGPIXELSX = 88
	        Private Const LOGPIXELSY = 90
	        Private Const PHYSICALWIDTH = 110
	        Private Const PHYSICALHEIGHT = 111
	        Private Const PHYSICALOFFSETX = 112
	        Private Const PHYSICALOFFSETY = 113
	
	        Private Sub PrintHeader(PrintTitle As Boolean, Margins As Long, _
	         LMargin As Long)
	         Dim BodyFontBold As Boolean, BodyFontSize As Integer
	         Dim BodyFontItalic As Boolean, HeaderLine As String
	         Dim PrtPositionX As Integer, PrtPositionY As Integer
	
	         If PrintTitle Then ' Only Print Title on first Page
	            PrtPositionX = Printer.Width / 2  ' center of page
	            ' Save any attributes you change for the header...
	            BodyFontBold = Printer.Font.Bold
	            BodyFontSize = Printer.Font.Size
	            ' Change the font for the header...
	            Printer.Font.Size = 16
	            Printer.Font.Bold = True
	            ' Print header lines...
	            HeaderLine = "Title of This Test Report"
	            ' Center Report title
	            Printer.CurrentX = PrtPositionX - (LMargin + _
	              Printer.TextWidth(HeaderLine) / 2)
	            Printer.Print HeaderLine
	            ' Reset the font...
	            Printer.Font.Size = BodyFontSize
	            Printer.Font.Bold = BodyFontBold
	         Else
	            Printer.NewPage   ' Otherwise we are at the bottom of a page
	         End If
	         PrtPositionY = Printer.CurrentY  ' remember this line
	         BodyFontItalic = Printer.Font.Italic
	         Printer.Font.Italic = True
	         Printer.Print "My very nice, Visual Basic report"
	         Printer.Font.Italic = BodyFontItalic
	         HeaderLine = Format(Date, "Long Date")
	         ' Right justify today's date
	         Printer.CurrentX = Printer.Width - (Margins + _
	            Printer.TextWidth(HeaderLine))
	         Printer.CurrentY = PrtPositionY  ' return to previous line
	         Printer.Print HeaderLine
	        End Sub
	
	        Private Sub PrintFooter(LastLine As Integer, _
	           LineHeight As Integer, LMargin As Long)
	         Dim PrtPositionX As Integer, PrintText As String
	         Static PageNum As Integer
	
	         PageNum = PageNum + 1
	         PrtPositionX = Printer.Width / 2   ' center of page
	         ' Move to the end of the page to print the Page Footer:
	         ' LastLine is where there is only room for one more line.
	         ' Set CurrentY to LastLine minus LineHeight times the number of
	         ' additional lines in the Footer.
	         Printer.CurrentY = LastLine - LineHeight  ' for 2 footer lines
	         PrintText = "Sample Page Footer"
	         ' Print the Footer text centered
	         Printer.CurrentX = PrtPositionX - (LMargin + _
	            Printer.TextWidth(PrintText) / 2)
	         Printer.Print PrintText
	         PrintText = "This is Page " & CStr(PageNum) & " of Test Report"
	         Printer.CurrentX = PrtPositionX - (LMargin + _
	            Printer.TextWidth(PrintText) / 2)
	         Printer.Print PrintText
	        End Sub
	
	        Private Function GetLargeString() As String
	         Dim BaseString As String, I As Integer
	
	         BaseString = "This is just a fairly long string to demonstrate how "
	         BaseString = BaseString & "to wrap text to impose your own right "
	         BaseString = BaseString & "margin.  "
	         For I = 1 To 2   ' See Q298825 to use a larger String
	           BaseString = BaseString & BaseString
	         Next I
	         GetLargeString = BaseString
	        End Function
	
	        Private Sub Command1_Click()
	        Dim dpiX As Long, dpiY As Long
	        Dim MarginLeft As Long, MarginRight As Long
	        Dim MarginTop As Long, MarginBottom As Long
	        Dim PrintAreaHorz As Long, PrintAreaVert As Long
	        Dim PhysHeight As Long, PhysWidth As Long
	        Dim Info As String
	
	        dpiX = GetDeviceCaps(Printer.hdc, LOGPIXELSX)
	        Info = "Pixels X: " & dpiX & " dpi"
	
	        dpiY = GetDeviceCaps(Printer.hdc, LOGPIXELSY)
	        Info = Info & vbCrLf & "Pixels Y: " & dpiY & " dpi"
	
	        MarginLeft = GetDeviceCaps(Printer.hdc, PHYSICALOFFSETX)
	        Info = Info & vbCrLf & "Unprintable space on left: " & _
	        MarginLeft & " pixels = " & MarginLeft / dpiX & " inches"
	
	        MarginTop = GetDeviceCaps(Printer.hdc, PHYSICALOFFSETY)
	        Info = Info & vbCrLf & "Unprintable space on top: " & _
	        MarginTop & " pixels = " & MarginTop / dpiY & " inches"
	
	        PrintAreaHorz = GetDeviceCaps(Printer.hdc, HORZRES)
	        Info = Info & vbCrLf & "Printable space (Horizontal): " & _
	        PrintAreaHorz & " pixels = " & PrintAreaHorz / dpiX & " inches"
	
	        PrintAreaVert = GetDeviceCaps(Printer.hdc, VERTRES)
	        Info = Info & vbCrLf & "Printable space (Vertical): " & _
	        PrintAreaVert & " pixels = " & PrintAreaVert / dpiY & " inches"
	
	        PhysWidth = GetDeviceCaps(Printer.hdc, PHYSICALWIDTH)
	        Info = Info & vbCrLf & "Total space (Horizontal): " & _
	        PhysWidth & " pixels = " & PhysWidth / dpiX & " inches"
	
	        MarginRight = PhysWidth - PrintAreaHorz - MarginLeft
	        Info = Info & vbCrLf & "Unprintable space on right: " & _
	        MarginRight & " pixels = " & MarginRight / dpiX & " inches"
	
	        PhysHeight = GetDeviceCaps(Printer.hdc, PHYSICALHEIGHT)
	        Info = Info & vbCrLf & "Total space (Vertical): " & _
	        PhysHeight & " pixels = " & PhysHeight / dpiY & " inches"
	
	        MarginBottom = PhysHeight - PrintAreaVert - MarginTop
	        Info = Info & vbCrLf & "Unprintable space on bottom: " & _
	        MarginBottom & " pixels = " & MarginBottom / dpiY & " inches"
	
	        MsgBox Info, , "GetDeviceCaps Returned the Following:"
	        End Sub
	
	        Private Sub Command2_Click()
	        Dim FooterLines As Integer, TextLine As String
	        Dim LineHeight As Integer, LastLine As Integer
	        Dim TotWidth As Long, TotHeight As Long
	        Dim MarginTop As Long, MarginBottom As Long
	        Dim TotalPrtAreaVert As Long, TotalPrtAreaHorz As Long
	        Dim MarginLeft As Long, MarginRight As Long
	        Dim LeftMargin As Long, HorzMargins As Long
	        Dim Line As Integer, RptHeaderPrint As Boolean
	        Dim BreakPoint As Integer, PrintLength As Integer
	        Dim TempString As String, CharLength As Integer
	        Dim WrapPoint As Integer, EstWrapPoint As Integer
	
	        Printer.Font.Name = "Arial"
	        Printer.Font.Size = 12
	
	        ' The next 8 values are in Pixels.
	        ' TotalPrtAreaVert is eqivalent to Printer.ScaleHeight
	        TotalPrtAreaVert = GetDeviceCaps(Printer.hdc, VERTRES)
	        TotHeight = GetDeviceCaps(Printer.hdc, PHYSICALHEIGHT)
	        MarginTop = GetDeviceCaps(Printer.hdc, PHYSICALOFFSETY)
	        MarginBottom = TotHeight - TotalPrtAreaVert - MarginTop
	        ' TotalPrtAreaHorz is eqivalent to Printer.ScaleWidth
	        TotalPrtAreaHorz = GetDeviceCaps(Printer.hdc, HORZRES)
	        TotWidth = GetDeviceCaps(Printer.hdc, PHYSICALWIDTH)
	        MarginLeft = GetDeviceCaps(Printer.hdc, PHYSICALOFFSETX)
	        MarginRight = TotWidth - TotalPrtAreaHorz - MarginLeft
	
	        HorzMargins = (MarginRight + MarginLeft) * Printer.TwipsPerPixelX
	        LeftMargin = MarginLeft * Printer.TwipsPerPixelX
	        ' Covert to twips for ease of use
	        TotalPrtAreaHorz = TotalPrtAreaHorz * Printer.TwipsPerPixelX
	        LineHeight = Printer.TextHeight("Test")
	        FooterLines = 2   ' number of lines in footer
	        LastLine = TotalPrtAreaVert * Printer.TwipsPerPixelY - LineHeight
	        ' Set the break point a line high so we can check it after printing
	        BreakPoint = LastLine - LineHeight * FooterLines
	        ' reduce the right margin by 1 inch, which is 1440 twips
	        PrintLength = TotalPrtAreaHorz - 1440
	
	        PrintHeader True, HorzMargins, LeftMargin  ' Report Header
	        RptHeaderPrint = False
	        ' Print the Footer when the current Y position >=
	        ' LastLine - LineHeight * <Number Of Lines In Footer>
	        For Line = 1 To 120
	           If RptHeaderPrint Then
	              PrintHeader False, HorzMargins, LeftMargin  ' Page Header
	              RptHeaderPrint = False
	           End If
	           TextLine = "This is line " & Line
	           ' To indent or set a new left margin, reset CurrentX before each
	           ' new line.
	           ' To use a new right margin, wrap lines at appropriate points.
	           If Line >= 10 And Line <= 14 Then
	              TextLine = TextLine & " indented."
	              Printer.CurrentX = 2 * 1440  ' indent 2 additional inches
	           ElseIf Line >= 48 And Line <= 52 Then
	              TextLine = GetLargeString()  ' Need String long for demo
	           End If
	           ' Use TotalPrtAreaHorz to use the default right margin
	           ' or use your own value for PrintLength for a custom right margin
	           ' in this example we bring in the right margin by 1 inch
	           If Printer.TextWidth(TextLine) > PrintLength Then  ' Wrap text
	              ' This estimating technique is used for simplicity
	              ' First, approximate character length
	              CharLength = Printer.TextWidth("aeiou.") / 6
	              ' Where to start looking for a line break (wrap)
	              EstWrapPoint = PrintLength / CharLength
	              WrapPoint = EstWrapPoint
	              Line = Line - 1  ' Since current line has already been counted
	
	              Do While Len(TextLine) > EstWrapPoint
	                 TextLine = Trim(TextLine)   ' remove spaces from either end
	                 ' break on a space near the estimated break point
	                 Do While InStr(WrapPoint, TextLine, " ") <> WrapPoint
	                    WrapPoint = WrapPoint - 1
	                 Loop
	                 TempString = Mid(TextLine, 1, WrapPoint)  ' what will fit
	                 Printer.Print Trim(TempString)  ' print what will fit
	                 TextLine = Mid(TextLine, WrapPoint + 1) ' get remaining text
	                 WrapPoint = EstWrapPoint  ' Reset the estimated wrap point
	                 Line = Line + 1  ' Increment line counter
	                 If Printer.CurrentY >= BreakPoint Then  ' another line?
	                    PrintFooter LastLine, LineHeight, LeftMargin
	                    If Len(TextLine) > 0 Then  ' Print header if text remains
	                       PrintHeader False, HorzMargins, LeftMargin
	                    End If
	                 End If
	              Loop
	              If Len(TextLine) > 0 Then  ' leftover text?
	                 Printer.Print TextLine
	                 Line = Line + 1  ' Increment line counter
	                 If Printer.CurrentY >= BreakPoint Then  ' another line?
	                    PrintFooter LastLine, LineHeight, LeftMargin
	                    RptHeaderPrint = True  ' Print Header if more lines
	                 End If
	              End If
	           Else
	              Printer.Print TextLine
	              If Printer.CurrentY >= BreakPoint Then
	                 PrintFooter LastLine, LineHeight, LeftMargin
	                 RptHeaderPrint = True  ' Print Header if more lines
	              End If
	           End If
	        Next Line
	        If Printer.CurrentY > 0 Then
	           PrintFooter LastLine, LineHeight, LeftMargin  ' For last page
	        End If
	        Printer.EndDoc   ' Finish
	        MsgBox "Check Printer for results.", , "Done!"
	        End Sub
	
	3. Run the project.
	
	4. Click Command1. You will see a message box listing the margins and printable
	  area of the page.
	
	5. Click Command2. Several pages are printed. The printing includes:
	
	  Report Header - Only printed at the top of page 1.
	
	  Page Header - Consists of some text printed in italics and the current date
	  right-justified on the page. Printed on all pages.
	
	  Page Footer - Consists of some text and a page number printed on multiple
	  lines. Printed on all pages.
	
	  Additionally, lines numbered 10 through 14 are indented an additional 2 inches
	  and lines numbered 48 through 56 demonstrate enforcing a custom right margin.
	
	For additional information about using the TextWidth method with large strings,
	click the article number below to view the article in the Microsoft Knowledge
	Base:
	
	  Q298825 PRB: Run-time Error '6' When You Use the TextWidth Method
	
	(c) Microsoft Corporation 1998, All Rights Reserved. Contributions by Chris E.
	Jolley, Microsoft Corporation.
	
	
	Additional query words:
	
	======================================================================
	Keywords          : kbprint kbAPI kbPrinting kbVBp kbVBp400 kbVBp500 kbVBp600 kbGrpDSVB 
	Technology        : kbVBSearch kbAudDeveloper kbZNotKeyword6 kbZNotKeyword2 kbVB500Search kbVB600Search kbVB500 kbVB600 kbVB400Search kbVB400
	Version           : :4.0,5.0,6.0
	Issue type        : kbhowto
	
	=============================================================================
	

{% endraw %}
