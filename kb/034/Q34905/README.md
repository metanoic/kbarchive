---
layout: page
title: "Q34905: Array Reference Gives &quot;C4046 '&amp;' on Function/Array, Ignored&quot;"
permalink: /kb/034/Q34905/
---

## Q34905: Array Reference Gives &quot;C4046 '&amp;' on Function/Array, Ignored&quot;

{% raw %}

	Article: Q34905
	Product(s): See article
	Version(s): 5.00 5.10 | 5.10
	Operating System(s): MS-DOS | OS/2
	Keyword(s): ENDUSER | | mspl13_c
	Last Modified: 26-AUG-1988
	
	The following compiler warning message occurs when an array is
	referred to incorrectly by the address-of operator (&).
	
	C4046 '&' on function/array, ignored
	
	The following program causes the warning C4046:
	
	void main(void);
	void main(void)
	{
	 char array[10];
	 char *ptr_to_array;
	 ptr_to_array = &array;
	}
	
	To clear up the warning, make the assignment read either
	
	ptr_to_array = array;
	
	or
	
	ptr_to_array = &array[0];
	
	More information about arrays can be found in the last paragraph on
	Page 104 and in Example 1 on Page 119 of the "Microsoft C Optimizing
	Compiler Language Reference" manual.

{% endraw %}
