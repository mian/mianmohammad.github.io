---
layout: post
title:  Character Encoding in Depth
tags:
- programming
- encoding
- ascii
---

<b>Character Encoding in Depth</b>
<p>
A character encoding is a mechanism which tells the computer how to interpret raw zeroes and ones into real characters. How the computer do it basically it does by pairing numbers with characters
</p>
<b>History:</b>
<p>If we talk about the beginning there were only dots and dashed and it was the earliest form of character set and encoding that was used by Morse for the telegraph in 1844 when he sent his first message.His code was first attempt to represent the alphabetic characters as a series of bits.
</p>
<p>Later In June 1963, on the basis of the <a href="https://en.wikipedia.org/wiki/Fieldata" target="_blank">FIELDATA</a> codes, the American Standards Institute created the ASCII-63 standard (American Standard Code for Information Interchange). ASCII-63 is almost recognizable to us, the control codes are all below 0x20, space is 0x20 and then follow the numbers, punctuation and upper case characters (with “A” as 0x41). The only glaring omission in ASCII-63 is that there are no lower case characters.
</p>
<p>
Then in October 1963 the ISO standards body decided that world need lower case characters also then lower case characters were added in it and apart from that some minor changes were also made to the punctuation characters and released the standard as ECMA-6.
</p>
<p>
In 1967 the ASA adopted the ECMA-6 and they released it as ASCII-1967, a 7-bit code containing 128 character codes that has remained in use until today.
</p>

<b>What is an encoding?</b>

<p>Look at the string 
<pre>
<code>
hello
</code>
</pre>
in bytes</p>
<pre><code>
$byte_array = unpack('C*', 'hello');
var_dump($byte_array);
[ 104, 101, 108, 108, 111 ]
</code></pre>

<p>So For the string hello the encoding is like this 
h=104 , e= 101, l=108, l=108, o=111</p>

<p>Now lets see the encoding for 
<pre><code>hellṏ</code></pre></p>

<pre><code>
$byte_array = unpack('C*', 'hellṏ');
var_dump($byte_array);
[ 104 , 101 , 108 , 108 , 225 , 185 , 143 ]
</code>
</pre>

<p>
Now we see that it takes more than one byte to represent 
<pre><code>"ṏ"</code></pre>
Three in fact: [225, 185, 143]. The encoding of a string defines this relationship: encoding is a map between one or more bytes and a displayable character.
</p>

<b>ASCII is fundamental:</b>
<p>Originally 1 character was always stored as 1 byte. A byte (8 bits) has the potential to distinct 256 possible values. But in fact only the first 7 bits were used. So only 128 characters were defined. This set is known as the ASCII character set.
</p>
<p>
0x00 - 0x1F contain steering codes (e.g. CR, LF, STX, ETX, EOT, BEL, ...)<br/>
0x20 - 0x40 contain numbers and punctuation<br/>
0x41 - 0x7F contain mostly alphabetic characters<br/>
0x80 - 0xFF the 8th bit = undefined<br/>
</p>




