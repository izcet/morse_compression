# On the subject of encoding characters in morse code into binary
A study into the feasibility of encoding ascii readable characters into morse code to save disk space.
<br><br>
At first glance, it would seem as though binary encoding and morse code would go hand in hand. After all, they are both systems that contain two digits (0 and 1) and (. and -). However, morse code also uses a specific timing sequence to differentiate the two, whereas binary is stored in bytes, collections of 8 bits stored in blocks.
<br>

```
A dot is represented as '.', or as a single tone length of 1.
A dash is represented as '-', or as a single tone of length 3 or three tones of length 1.
A gap between dots and dashes within a single letter is a silence of length 1.
A gap between letters is a silence of length 3.
```

<br>
As you can see from the above excerpt, morse code is actually comprised of two bits of data: the state (on or off, noise or silence) and length (1 or 3, short or long).
<br>
To translate morse code into binary, each peice of information as a dot or a dash would take up two bits of information. One for the state, and one for the length.
<br>
<br>
I went and broke up each part of the morse encoding into a binary equivalent. Unfortunately, I came up with the binary codes while just whiteboarding a shower thought, not with the same rigor, thought, and verbosity that I'm putting into this readme. If I'd done it correctly the first time, the pattern might look something like this:
<br>

```
First bit	-	noise	-	off or on
Second bit	-	length	-	short or long

Example:

DOT	(.)		-	10
DASH (-)		-	11
END OF CHARACTER	-	00	// not a literal translation, short gap is usually between dots and dashes, not full characters
SPACE (between words)	-	01
```

<br><br>
However, the actual pattern I went with is only slightly different.

```
DOT				-	01
DASH				-	11
END OF CHARACTER		-	10
SPACE				-	00
```

<br>
This results in the table below.
<br><br>
 - Char represents the ascii character.
 - Morse is the literal morse code
 - Binary is the representation of the morse code in my "binary" system.
 - Bits is the number of bits that the character occupies (before/after EOC)
 - The symbols in the size column have to do with greater or less space usage, as compared to a byte (8 bits). A single minus represents 2 bits of saving after EOC, a single plus represents 2 bits excess usage after EOC. Additional characters are another 2 bits in the respective direction.

```
CHAR	MORSE		 BINARY					BITS	SIZE

A		.-			 0111[10]				4/6		-
B		-...		 11010101[10]			8/10	+
C		-.-.		 11011101[10]			8/10	+
D		-..			 110101[10]				6/8		
E		.			 01[10]					2/4		--
F		..-.		 01011101[10]			8/10	+
G		--.			 111101[10]				6/8		
H		....		 01010101[10]			8/10	+
I		..			 0101[10]				4/6		-
J		.---		 01111111[10]			8/10	+
K		-.-			 110111[10]				6/8		
L		.-..		 01110101[10]			8/10	+
M		--			 1111[10]				4/6		-
N		-.			 1101[10]				4/6		-
O		---			 111111[10]				6/8		
P		.--.		 01111101[10]			8/10	+
Q		--.-		 11110111[10]			8/10	+
R		.-.			 011101[10]				6/8		
S		...			 010101[10]				6/8		
T		-			 11[10]					2/4		--
U		..-			 010111[10]				6/8		
V		...-		 01010111[10]			8/10	+
W		.--			 011111[10]				6/8		
X		-..-		 11010111[10]			8/10	+
Y		-.--		 11011111[10]			8/10	+
Z		--..		 11110101[10]			8/10	+

0		-----		 1111111111[10]			10/12	++
1		.----		 0111111111[10]			10/12	++
2		..---		 0101111111[10]			10/12	++
3		...--		 0101011111[10]			10/12	++
4		....-		 0101010111[10]			10/12	++
5		.....		 0101010101[10]			10/12	++
6		-....		 1101010101[10]			10/12	++
7		--...		 1111010101[10]			10/12	++
8		---..		 1111110101[10]			10/12	++
9		----.		 1111111101[10]			10/12	++

Ä		.-.-		 01110111[10]			8/10	+
Á		.--.-		 0111110111[10]			10/12	++
Å		.--.-		 0111110111[10]			10/12	++
Ch		----		 11111111[10]			8/10	+
É		..-..		 0101110101[10]			10/12	++
Ñ		--.--		 1111011111[10]			10/12	++
Ö		---.		 11111101[10]			8/10	+
Ü		..--		 01011111[10]			8/10	+
 		
.		.-.-.-		 011101110111[10]		12/14	+++
,		--..--		 111101011111[10]		12/14	+++
:		---...		 111111010101[10]		12/14	+++
?		..--..		 010111110101[10]		12/14	+++
'		.----.		 011111111101[10]		12/14	+++
/		-..-.		 1101011101[10]			10/12	++
()		-.--.-		 110111110111[10]		12/14	+++
"		.-..-.		 011101011101[10]		12/14	+++
@		.--.-.		 011111011101[10]		12/14	+++
=		-...-		 1101010111[10]			10/12	++
 		
\n		.-.-		 01110111[10]			8/10	+
``` 
