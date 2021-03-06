---
layout: page
title: "Q262126: XCON: Using Imccopy.exe for Internet Mail Service Message Format"
permalink: /kb/262/Q262126/
---

## Q262126: XCON: Using Imccopy.exe for Internet Mail Service Message Format

{% raw %}

	Article: Q262126
	Product(s): Microsoft Exchange
	Version(s): winnt:5.5
	Operating System(s): 
	Keyword(s): exc55
	Last Modified: 06-AUG-2002
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Exchange Server, version 5.5 
	-------------------------------------------------------------------------------
	
	SUMMARY
	=======
	
	You can use the Imccopy.exe utility to extract information about the Internet
	Mail Service. This article describes how to decode the message formatting
	options on the Internet Mail Service by using the output of Imccopy.exe.
	
	MORE INFORMATION
	================
	
	Imccopy.exe is located on the Exchange Server CD-ROM in the
	Server\Support\Utils\platform folder.
	
	Copy the Imccopy.exe file to drive C, open a command prompt, and at drive C run
	the imccopy -save domain imc.txt command. The Imc.txt file is similar to the
	following:
	
	  
	
	  [Header]
	  Version=1
	
	  [Domain]
	  DomainInformation=+
	  +Default,ISO-8859-1,ISO-8859-1,800,76,0,0,0
	  +microsoft.com,ISO-8859-1,ISO-8859-1,800,76,0,0,0
	
	The Format of the Output
	------------------------
	
	This information in the Imc.txt file is divided (by commas) into the fields in
	the following table.
	
	  
	
	  ---------------------------------------------------------------------------
	  Domain   Mime         Non-Mime    Formatting   Word   Send  Unused  Message
	        Character    Character   Information  Wrap   Rich          Size
	        Set          Set         (See         at     Text          Limit
	                                 Following    Column
	                                 Table)
	  ---------------------------------------------------------------------------
	  Default  ISO-8859-1  ISO-8859-1   800          76     0      0       0
	  ---------------------------------------------------------------------------
	
	Output Table Explanation:
	
	- Domain. This is the domain for which the options are set. You should always
	  have a Default domain, but you may not have any other domains if you have not
	  specified any under the Specify by E-Mail Domain option on the Internet Mail
	  tab of the Internet Mail Service.
	
	- Mime Character Set. This is the character set that is specified on the
	  Internet Mail tab for Multipurpose Internet Mail Extensions (MIME) messages.
	
	- Non-Mime Character Set. This is the character set that is specified on the
	  Internet Mail tab for non-MIME messages.
	
	- Formatting Information. Decimal representation of a binary number for which
	  certain bits set certain formatting options. See the following table for
	  information about how to decode these representations.
	
	- Word Wrap at Column. This field is the "Message text word wrap at column"
	  setting (to locate this setting, click "Advanced options" on the Internet
	  Mail tab).
	
	- Send Rich Text. This field is the "Send Microsoft Exchange rich text
	  formatting" setting (to locate this setting, click "Advanced options" on the
	  Internet Mail tab). This setting has the following three options:
	
	   - 0=User
	
	   - 1=Always
	
	   - 2=Never
	
	- Message Size Limit. This is the "Maximum message size" setting that is
	  specified under "Specify by E-Mail Domain" on the Internet Mail tab of the
	  Internet Mail Service. This setting is only valid if you specify the setting
	  for each domain. If there is a message size limit specified on the General
	  tab of the Internet Mail Service, the message size limit is not included in
	  the Imccopy output.
	
	Decoding the Formatting Information
	-----------------------------------
	
	Imccopy.exe reports the formatting information as a decimal number. To decode
	this information you need to convert the decimal number to a binary number. You
	can do this by using the Microsoft Windows Calculator utility.
	
	For example, in the sample output in the beginning of this section, Imccopy
	reported that the formatting information is the decimal number 800. If you
	convert this to a binary number, it becomes 11 0010 0000. Certain bits in this
	binary number represent specific settings.
	
	The following table lists the bits from top to bottom as they appear in the
	binary number from right to left (for example, the rightmost bit in the number
	corresponds to the first entry in this table).
	
	+-------------------------------------------------+
	| Bit | Setting                                   | 
	+-------------------------------------------------+
	| 0   | Unused                                    | 
	+-------------------------------------------------+
	| 1   | Word Wrap Set                             | 
	+-------------------------------------------------+
	| 1   | Disable Sending Display Name to Internet  | 
	+-------------------------------------------------+
	| 0   | Unused                                    | 
	+-------------------------------------------------+
	| 1   | UUENCODE                                  | 
	+-------------------------------------------------+
	| 1   | MIME with Plain Text Only                 | 
	+-------------------------------------------------+
	| 1   | Binhex                                    | 
	+-------------------------------------------------+
	| 0   | Unused                                    | 
	+-------------------------------------------------+
	| 1   | Disable Out of Office Replies to Internet | 
	+-------------------------------------------------+
	| 1   | Disable AutoReplies to Internet           | 
	+-------------------------------------------------+
	| 0   | Unused                                    | 
	+-------------------------------------------------+
	| 0   | Unused                                    | 
	+-------------------------------------------------+
	| 0   | Unused                                    | 
	+-------------------------------------------------+
	| 0   | Unused                                    | 
	+-------------------------------------------------+
	| 0   | Unused                                    | 
	+-------------------------------------------------+
	| 0   | Unused                                    | 
	+-------------------------------------------------+
	| 1   | MIME with HTML Only                       | 
	+-------------------------------------------------+
	| 1   | MIME with HTML and Plain Text             | 
	+-------------------------------------------------+
	
	Bit and Setting Table Explanation:
	
	- Word Wrap Set. This bit is set if you click "At column" under "Message text
	  word wrap" (to locate this setting, click "Advanced options" on the Internet
	  Mail tab).
	
	- Disable Sending Display Name to Internet. This bit is set if you click to
	  select the "Disable sending Display names to the Internet" check box (to
	  locate this setting, click "Advanced options" on the Internet Mail tab).
	
	- UUENCODE. This bit is set if you click UUENCODE under Message Content on the
	  Internet Mail tab. If this bit is set, none of the MIME bits can be set,
	  because MIME and UUENCODE are mutually exclusive in this situation.
	
	- MIME with Plain Text Only. This bit is set if you click "MIME" and click to
	  select only the Plain text check box under Message Content on the Internet
	  Mail tab. If this bit is set, the following bits cannot be set: UUENCODE,
	  Binhex, MIME with HTML Only.
	
	- Binhex. This bit is set if you click to select the Binhex check box under
	  Message Content on the Internet Mail tab. The UUENCODE bit must be set to set
	  this bit.
	
	- Disable Out of Office Responses to Internet. This bit is set if you click to
	  select the "Disable Out of Office responses to the Internet" check box (to
	  locate this setting, click "Advanced options" on the Internet Mail tab).
	
	- Disable Auto Replies to Internet. This bit is set if you click to select the
	  "Disable Automatic Replies to the Internet" check box (to locate this
	  setting, click "Advanced options" on the Internet Mail tab).
	
	- MIME with HTML Only. This bit is set if you click MIME and click to select
	  only the HTML check box under Message Content on the Internet Mail tab. If
	  this bit is set, the following bits cannot be set: UUENCODE, Binhex, MIME
	  with Plain Text Only.
	
	- MIME with HTML and Plain Text. This bit is set if you click MIME and click to
	  select both the "Plain text" and HTML check boxes under Message Content on
	  the Internet Mail tab. If this bit is set, the following bits cannot be set:
	  UUENCODE, Binhex, MIME with Plain Text Only, MIME with HTML Only.
	
	Additional query words: extension-data, imccopy
	
	======================================================================
	Keywords          : exc55 
	Technology        : kbExchangeSearch kbExchange550 kbZNotKeyword2
	Version           : winnt:5.5
	Issue type        : kbinfo
	
	=============================================================================
	

{% endraw %}
