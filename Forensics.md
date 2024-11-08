# m00nwalk

**Flag:** : `picoCTF{beep_boop_im_in_space}`

How you approached the challenge:

- Researched SSTV and QSSTV
- Installed QSSTV and Pavucontrol on WSL
- Learned and accessed files from windows on WSL
- decoded the audio file using QSSTV

```
k4ngroo@Laptop-lol:~$ cd /mnt/c/Users/anant/OneDrive/Desktop/Anant/Cryptonite
k4ngroo@Laptop-lol:/mnt/c/Users/anant/OneDrive/Desktop/Anant/Cryptonite$ paplay -d virtual-cable message.wav
```

```
terminal output
```

- etc.

![screenshot](C:\Users\anant\OneDrive\Desktop\Anant\Cryptonite\QSSTV.png)

What you learned through solving this challenge:

1. Improved skills on WSL and Ubuntu using commands like apt-get 
2. SSTV and QSSTV

Other incorrect methods you tried:

- Tried searching for audio file Metadata
- generally took a lot of time to install all the required packages

References

- https://ourcodeworld.com/articles/read/956/how-to-convert-decode-a-slow-scan-television-transmissions-sstv-audio-file-to-images-using-qsstv-in-ubuntu-18-04
- stackoverflow.com
