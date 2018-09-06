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

<p>
French, German and many other languages needed additional characters. (e.g. à, é, ç, ô, ...) which were not available in the ASCII character set. So they used the 8th bit to define their characters. This is what is known as "extended ASCII".
</p>

<p>The problem is that the additional 1 bit has not enough capacity to cover all languages in the world. So each region has his own ASCII variant. There are many extended ASCII encodings (latin-1being a very popular one).
</p>

<p>
Popular question: “Is ASCII a character set or is it an encoding” ? ASCII is a character set. However, in programming charset and encoding are wildly used as synonyms. If I want to refer to an encoding that only contains the ASCII characters and nothing more (the 8th bit is always 0): that's US-ASCII
</p>

<p>These are following terms applied to character sets:</p>

<p>The following terms apply to character encodings:</p>

<p>SBCS Single-byte character set; a character set encoded in one byte per character, such as ASCII or ISO 8859–1.</p>

<p>DBCS Double-byte character set; a method of encoding a character set in no more than 2 bytes, such as Shift-JIS. Many character encoding schemes that are referred to as double-byte, including Shift-JIS, allow mixing of single-byte and double-byte encoded characters. Others, such as UCS-2, use 2 bytes for all characters.
</p>

<p>MBCS Multiple-byte character set; a character set encoded with a variable number of bytes per character, such as UTF-8.The following table lists some common character encodings; however, there are many additional character encodings that browsers and web servers support:
</p>

<p>
<img src="https://cdn-images-1.medium.com/max/1600/1*3XynzglHm3-iRjmkhU25gg.png" width="60%">
</p>

<p>
The World Wide Web Consortium maintains a list of all character encodings supported by the Internet. You can find this information at 
<a href="www.w3.org/International/O-charset.html" target="_blank">www.w3.org/International/O-charset.html</a>
</p>

<b>Encoding in Web Pages</b>

<p>Let me do some insights how the web page actually works.</p>
<p>So web pages are served using HTTP (HyperText Transfer Protocol) means when a browser sends request via HTTP then in the response the server send response via HTTP. And this response consists of two parts headers and body.The header provides information about the content (body).
</p>

<p>For HTML , encoding information should be sent by using the Content-Type header</p>

<pre><code>
Content-Type: text/html; charset=utf-8
</code></pre>

<p>You can also provide an HTTP equivalent in HTML that will enable the encoding when the page is viewed offline. You can achieve it by using a META element in the HEAD-section of your document:
</p>

<pre><code>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8"/>
</code></pre>

<p>Apache Server is one of the most commonly used servers to serve web pages</p>

<p>To Enable the UTF-8 encoding by default in Apache You will need to modify the .htaccess file on your Apache instance to set this.
</p>

<p>Open the .htaccess file in a text editor and modify it to include in it.</p>

<pre><code>AddDefaultCharset UTF-8</code></pre>

<p>Nginx is also a very popular web server. We can modify the response headers in the Nginx server in the config. Just open the file nginx.conf in your conf/ directory and add the following code.
</p>

<pre><code>charset UTF-8</code></pre>

<b>Conclusion</b>

<p>Web Pages have different options one such feature is character encoding which allows you to specify the character supported by page.So we can specify the character encoding for a web page in different ways including the HTTP headers or meta element.We need to always specify the character encoding so make sure the page is properly displayed.
</p>



