---
layout: post
title: Bitwise JavaScript
summary: .
tags: [code, javascript]
time: "22:15"
---

## JavaScript's Bitwise Operators.

Operator	Action	Example
&	bitwise AND	10&3=2
|	bitwise OR	10|3=11
^	bitwise exclusive OR	10^3=9
<<	left shift	10<<3=80
>>	Sign-propagating right shift	10>>3=1
>>>	Zero-fill right shift	10>>>3=1


### Modulus With Bitwise Masks

http://gala4th.blogspot.com/2009/04/modulus-with-bitwise-masks.html

16 - 15 (0x0F)
32 - 31 (0x1F)
64 - 63 (0x3F)
128 - 127 (0x7F)
256 - 255 (0xFF)

{% highlight javascript %}
45 % 32
45 & 31
45 & 0x1F

    00101101 (45)
AND 00011111 (31)
  = 00001101 (13)
45 % 32 = 13


//Lazy way
for(int i = 0, j = 0; i < 256; i++)
{
    if(j % 16 == 0) j = 0;
    else j++;
}

//Better way
for(int i = 0, j = 0; i < 256; i++)
{
    j++;
    j %= 16;
}

//Combine it into one line
for(int i = 0, j = 0; i < 256; i++)
{
    ++j %= 16;
}

//Combined using binary mask
for(int i = 0, j = 0; i < 256; i++)
{
    ++j &= 0xF;
}

{% endhighlight %}