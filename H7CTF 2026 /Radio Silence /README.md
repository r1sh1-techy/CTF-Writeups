# Radio Silence 
>this one was damn hard ngl and its 4:30 am rn :3

### Inspectrum

![inspectrum](https://github.com/r1sh1-techy/CTF-Writeups/blob/3763cc0371213f148f96812e37da97b20a5abbb7/H7CTF%202026%20/Radio%20Silence/inspectrum.png)

I opened the ``.cf32`` file in Inspectrum and set the sample rate to 1MHz as given.

By examining the signal's spectrum and frequency transitions, I identified two distinct frequency levels. 
This suggested that the transmission used Frequency-Shift Keying , where information is represented by switching between two frequencies.
>googled this ^ btw *hehe*

### Decoding with Cyberchef
I used the terminal to inspect the recording and work with the signal data.

The file contained complex floating-point IQ samples. Using the 1 MHz sample rate as the timing reference, the signal transitions could be analysed to determine the symbol timing.

The two frequency states were interpreted as binary values:

Lower frequency → 0

Higher frequency → 1

After identifying the symbol timing and reading the transmitted data, I obtained a binary sequence containing a preamble followed by the payload.
```
01001000 00110111 01000011 01010100
01000110 01111011 01100010 00110011
00111000 00111000 00111000 00111000
01100110 01100100 00101101 01100011
00110010 01100010 01100100 00101101
00110100 00110001 01100011 01100100
00101101 01100010 00110011 01100011
01100011 00101101 00110011 01100011
01100110 00111000 00111000 01100100
01100011 00110110 00110000 00110010
01100110 00110101 01111101
```

Once the payload had been extracted as binary data, I used CyberChef to convert it into readable ASCII text.


![flag](https://github.com/r1sh1-techy/CTF-Writeups/blob/3763cc0371213f148f96812e37da97b20a5abbb7/H7CTF%202026%20/Radio%20Silence/flag3.png)

Flag found:
```
H7CTF{b38888fd-c2bd-41cd-b3cc-3cf88dc602f5}
```

