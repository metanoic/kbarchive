---
layout: page
title: "Q288548: HOWTO: Override MQMD MSMQ-MQSeries Bridge Extension Fields in VB"
permalink: /kb/288/Q288548/
---

## Q288548: HOWTO: Override MQMD MSMQ-MQSeries Bridge Extension Fields in VB

{% raw %}

	Article: Q288548
	Product(s): Microsoft Visual Basic for Windows
	Version(s): 2000,6.0
	Operating System(s): 
	Keyword(s): kbref kbMSMQ kbDocs kbVBp400 kbVBp500 kbVBp600 kbMQSeriesBridge
	Last Modified: 05-JUN-2001
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Visual Basic Professional Edition for Windows, version 6.0 
	- Microsoft Visual Basic Enterprise Edition for Windows, version 6.0 
	- MSMQ - MQSeries Bridge 
	- the operating system: Microsoft Windows 2000 
	-------------------------------------------------------------------------------
	
	SUMMARY
	=======
	
	Microsoft Message Queuing Services (MSMQ-MQSeries) Bridge Extensions can be used
	to override the default MSMQ-MQSeries Bridge message property mapping. The
	sample in this article sends messages to MSMQ queue, overriding the default
	values for these MQ Message Descriptor (MQMD) extension fields.
	
	MORE INFORMATION
	================
	
	The following example creates a one-form Visual Basic project that shows how to
	override the default values for these MQMD extension fields.
	
	Step-by-Step Example
	--------------------
	
	1. Start Visual Basic and create a new Standard EXE project. Form1 is created by
	  default.
	
	2. On the Project menu, click to select References, and then add a reference to
	  the Microsoft Message Queue 2.0 Object Library.
	
	3. Add a CommandButton onto the form.
	
	4. Add the following code to your form:
	
	  Option Explicit
	  'A message extension is an MSMQ message property of arbitrary length.
	  'A message extension is a sequential buffer containing any number of
	  'MSMQ extension fields.
	
	  'Each extension field comprises three subfields:
	
	  'GUID   16 Bytes - A GUID identifier, typically of the application that created the extension field.
	  'Length 4 Bytes  - The Length of the Data subfield in bytes.
	  'Data Value of the length subfield Any data that is part of the message extension.
	
	  Private Declare Sub CopyMemory Lib "KERNEL32" Alias "RtlMoveMemory" ( _
	               hpvDest As Any, hpvSource As Any, ByVal cbCopy As Long)
	
	  Private Type GUID
	     Data1 As Long
	     Data2 As Integer
	     Data3 As Integer
	     Data4(7) As Byte
	  End Type
	
	  Private Type MQMD
	      StrucId(3) As Byte '/* Structure identifier */ 
	      Version As Long '/* Structure version number */ 
	      Report As Long '/* Report options */ 
	      MsgType As Long '/* Message type */ 
	      Expiry As Long '/* Expiry time */ 
	      Feedback As Long '/* Feedback or reason code */ 
	      Encoding As Long '/* Data encoding */ 
	      CodedCharSetId As Long '/* Coded character set identifier */ 
	      Format(7) As Byte '/* Format name */ 
	      Priority As Long '/* Message priority */ 
	      Persistence As Long '/* Message persistence */ 
	      MsgId(23) As Byte '/* Message identifier */ 
	      CorrelId(23) As Byte '/* Correlation identifier */ 
	      BackoutCount As Long 'Backout counter */ 
	      ReplyToQ(47) As Byte '/* Name of reply-to queue */ 
	      ReplyToQMgr(47) As Byte '/* Name of reply queue manager */ 
	      UserIdentifier(11) As Byte ' /* User identifier */ 
	      AccountingToken(31) As Byte '/* Accounting token */ 
	      ApplIdentityData(31) As Byte  '/* Application data relating to
	                                    'identity */ 
	      PutApplType As Long 'Type of application that put the
	                          'message */ 
	      PutApplName(27) As Byte '/* Name of application that put the
	                              'message */ 
	      PutDate(7) As Byte '/* Date when message was put */ 
	      PutTime(7) As Byte '/* Time when message was put */ 
	      ApplOriginData(3) As Byte '/* Application data relating to
	                                    'origin */ 
	      GroupId(23) As Byte       '/* Group identifier */ 
	      MsgSeqNumber As Long      '/* Sequence number of logical message <BR/>
	                                'within group */ 
	      Offset As Long            '/* Offset of data in physical message
	                                'from start of logical message */ 
	      MsgFlags As Long          '/* Message flags */ 
	      OriginalLength As Long    '/* Length of original message */ 
	  End Type
	
	     Private Sub Command1_Click()
	      'The MQMD extension has the following GUID for MQMD
	      ' {595B4981-8FBE-11d0-864D-00A024EDE0AF}
	      Dim tguid As GUID
	      tguid.Data1 = &H595B4981    '4 Bytes
	      tguid.Data2 = &H8FBE        '2 Bytes
	      tguid.Data3 = &H11D0        '2 Bytes
	      tguid.Data4(0) = &H86       '8 Bytes
	      tguid.Data4(1) = &H4D
	      tguid.Data4(2) = &H0
	      tguid.Data4(3) = &HA0
	      tguid.Data4(4) = &H24
	      tguid.Data4(5) = &HED
	      tguid.Data4(6) = &HE0
	      tguid.Data4(7) = &HAF
	      
	      Dim lenGUID As Long
	      lenGUID = LenB(tguid)
	
	      Dim tMQMD As MQMD
	
	      Dim lenMQMD As Long
	      lenMQMD = LenB(tMQMD)
	      CopyMemory tMQMD.StrucId(0), ByVal "MD  ", UBound(tMQMD.StrucId) + 1 
	      tMQMD.Version = 1&
	      tMQMD.MsgType = 8&
	      tMQMD.Expiry = -1&
	      tMQMD.Encoding = &H222&  'MQENC_NATIVE 0x00000222L
	      CopyMemory tMQMD.Format(0), ByVal "        ", UBound(tMQMD.Format) + 1
	      tMQMD.Priority = -1&
	      tMQMD.Persistence = 2& 'MQPER_PERSISTENCE_AS_Q_DEF
	      CopyMemory tMQMD.CorrelId(0), ByVal "AMQ!NEW_SESSION_CORRELID", _
	      UBound(tMQMD.CorrelId) + 1
	      CopyMemory tMQMD.ReplyToQ(0), ByVal "QUEUE", UBound(tMQMD.ReplyToQ) + 1
	      CopyMemory tMQMD.ReplyToQMgr(0), ByVal "MSBRIDGE1", _ 
	      UBound(tMQMD.ReplyToQMgr) + 1
	      tMQMD.MsgSeqNumber = 1&
	      tMQMD.OriginalLength = -1&
	      'Get size of Correlation ID data
	      Dim lSizeOfData As Long
	      Dim lenlSizeOfData As Long
	      lenlSizeOfData = LenB(lSizeOfData)
	      lSizeOfData = lenlSizeOfData + lenGUID + lenMQMD
	
	      'Fill Extension Byte Array
	      Dim ba() As Byte
	      ReDim ba(0 To lSizeOfData - 1)
	      
	      CopyMemory ba(0), lSizeOfData, LenB(lSizeOfData)
	      CopyMemory ba(lenlSizeOfData), tguid, lenGUID
	      CopyMemory ba(lenlSizeOfData + lenGUID), tMQMD, lenMQMD
	
	      'Send the message
	      Dim oQinfo As New MSMQ.MSMQQueueInfo
	      Dim oQ As MSMQ.MSMQQueue
	      
	      oQinfo.FormatName = "DIRECT=OS:MyServer\MyQueue"
	      Set oQ = oQinfo.Open(MQ_SEND_ACCESS, _
	                              MQ_DENY_NONE)
	      Dim oMessage As New MSMQ.MSMQMessage
	      oMessage.Extension = ba
	
	      'No need to translate message to EBCDIC
	      'The bridge will perform the translation
	      oMessage.Label = "Test"
	      oMessage.Body = "Test Body"
	      oMessage.Priority = 5
	      oMessage.Send oQ
	      oQ.Close
	  End Sub
	
	5. Verify that the properties are successfully overridden by using the MSDN
	  sample EPRecv.
	
	For more information on the EPRecv sample, see the following MSDN Web site at:
	
	  http://msdn.microsoft.com/library/psdk/his/bridappb_5rho.htm
	
	REFERENCES
	==========
	
	Host Integration Server 2000 Developers Guide "Building an MQSeries Message"
	
	Additional query words:
	
	======================================================================
	Keywords          : kbref kbMSMQ kbDocs kbVBp400 kbVBp500 kbVBp600 kbMQSeriesBridge 
	Technology        : kbOSWin2000 kbVBSearch kbAudDeveloper kbOSWinSearch kbZNotKeyword6 kbZNotKeyword2 kbVB600Search kbVB600 kbMSMQSearch kbMSMQ100
	Version           : :2000,6.0
	Issue type        : kbhowto
	
	=============================================================================
	

{% endraw %}
