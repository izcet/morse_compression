# On the subject of encoding characters in morse code into binary
A study into the feasibility of encoding ascii readable characters into morse code to save disk space.
<br><br>
At first glance, it would seem as though binary encoding and morse code would go hand in hand. After all, they are both systems that contain two digits (0 and 1) and (. and -). However, morse code also uses a specific timing sequence to differentiate the two, whereas binary is stored in bytes, collections of 8 bits stored in blocks.
<br>
```
A dot is represented as '.', or as a single tone length of 1.
A dash is represented as '-', or as a single tone of length 3 or three tones of length 1.
A gap between dots and dashes within a single letter is asilence of length 1.
A gap between letters is a silence of length 3.
```
<br>
As you can see from the above excerpt, morse code is actually comprised of two bits of data: the state (on or off, noise or silence) and length (1 or 3, short or long).
<br>
To translate morse code into binary, each peice of information as a dot or a dash would take up two bits of information. One for the state, and one for the length.
