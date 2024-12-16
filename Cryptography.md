# C3
**Flag:** 'adlibs'

## PROCEDURE
-I tried to reverse the algo in the encoder provided by changing the string.
-Took the character from lookup2 instead of lookup1
-changed cur-prev to cur+prev so that I add the value that was initially subtracted ig
-changed the value of prev from cur to (cur+prev)%40 to reverse the process 

```
import sys
chars = ""
from fileinput import input
for line in input():
  chars += line

lookup1 = "\n \"#()*+/1:=[]abcdefghijklmnopqrstuvwxyz"
lookup2 = "ABCDEFGHIJKLMNOPQRSTabcdefghijklmnopqrst"


out = ""

prev = 0
for char in chars:
  cur = lookup2.index(char)
  out += lookup1[(cur + prev) % 40]
  prev = (cur+prev)%40

print(out)
```

-ran the script received in output using Python2 as it mentioned python 2
-provided the script itself as the input to the script
-received the flag

```
#asciiorder
#fortychars
#selfinput
#pythontwo

chars = ""
from fileinput import input
for line in input():
    chars += line
b = 1 / 1

for i in range(len(chars)):
    if i == b * b * b:
        print chars[i] #prints
        b += 1 / 1
```

-flag received

```
a
d
l
i
b
s
```

![screenshot1](C:\Users\anant\OneDrive\Desktop\Anant\Cryptonite\C3SS1.png)
![screenshot2](C:\Users\anant\OneDrive\Desktop\Anant\Cryptonite\C3SS2.png)

## Concepts learned
1. Python
2. Mathematical application

## Incorrect Methods
1. Did not change the value of cur properly the first time
2. Provided the original cipher text as input to the second program

## References
- w3schools.com


  # Custom Encryption

**Flag:** `picoCTF{custom_d2cr0pt6d_e4530597}`

How you approached the challenge:

- divided all the numbers in the list by the key and 311. Changed these numbers into characters and added them into a string
- went through the received cipher text in reversed order of the plain text
- performed the normal decryption and followed it up with the xor decryption to get the text
- replaced the values in the calling of the test function to the appropiate values

```
import sys


def generator(g, x, p):
    return pow(g, x) % p




def is_prime(p):
    v = 0
    for i in range(2, p + 1):
        if p % i == 0:
            v = v + 1
    if v > 1:
        return False
    else:
        return True
def decrypt(cipher, key):
    txt1 = ""
    for i in cipher:
        a = i//(key*311)
        b = chr(int(a))
        txt1 = txt1 + b
    return txt1
def xor_decrypt(ciphertext, key):
    plain_text = ""
    key_length = len(key)
    for i, char in enumerate(ciphertext):
        key_char = key[i % key_length]
        decrypted_char = chr(ord(char) ^ ord(key_char))
        plain_text += decrypted_char
    return plain_text

def test(cipher_text, text_key):
    p = 97
    g = 31
    a = 97
    b = 22
    u = generator(g, a, p)
    v = generator(g, b, p)
    cipher = [151146, 1158786, 1276344, 1360314, 1427490, 1377108, 1074816, 1074816, 386262, 705348, 0, 1393902, 352674, 83970, 1141992, 0, 369468, 1444284, 16794, 1041228, 403056, 453438, 100764, 100764, 285498, 100764, 436644, 856494, 537408, 822906, 436644, 117558, 201528, 285498]
    key = generator(v, a, p)
    b_key = generator(u, b, p)
    shared_key = None
    if key == b_key:
        shared_key = key
    else:
        print("Invalid key")
        return
    semi_cipher = decrypt(cipher, shared_key)
    plain = xor_decrypt(semi_cipher, "trudeau" )
    
    print(plain[::-1])

if __name__ == "__main__":
    message = [151146, 1158786, 1276344, 1360314, 1427490, 1377108, 1074816, 1074816, 386262, 705348, 0, 1393902, 352674, 83970, 1141992, 0, 369468, 1444284, 16794, 1041228, 403056, 453438, 100764, 100764, 285498, 100764, 436644, 856494, 537408, 822906, 436644, 117558, 201528, 285498]
    test(message, "trudeau")

```

```
PS C:\Users\anant\OneDrive\Desktop\Anant\Cryptonite> python -u "c:\Users\anant\OneDrive\Desktop\Anant\Cryptonite\custom.py"
picoCTF{custom_d2cr0pt6d_e4530597}
```

![screenshot](C:\Users\anant\OneDrive\Desktop\Anant\Cryptonite\CustomEncryption1.png)
![screenshot](C:\Users\anant\OneDrive\Desktop\Anant\Cryptonite\CustomEncryption2.png)

What you learned through solving this challenge:

1. XOR Encrytion and decryption
2. Enumerate

Other incorrect methods you tried:

- Did not correctly order the decryption
- did not replace the values in the calling of the test fucntion resulting in no results

References

- www.101computing.net
- r/hacking
- medium.com



# MiniRSA

**Flag:** `picoCTF{n33d_a_lArg3r_e_606ce004}`

How you approached the challenge:

- created a function to calculate the cube root of ciphertext since the value of e=3 which is very small. The function uses Binary Search

```
def root(n):
    a = 1
    b = n
    while (b-a) > 1:
        mid = (a+b)//2
        if (mid**3)>n:
            b = mid
        else:
            a = mid
        
    if a**3 == n:
        return a
    elif b**3 == n:
        return b
    else:
        return 0
```

- changed the obtained value into hexadecimal and used the value to get the flag by decoding into UTF-8 using codecs

```
import math
import codecs

n= 29331922499794985782735976045591164936683059380558950386560160105740343201513369939006307531165922708949619162698623675349030430859547825708994708321803705309459438099340427770580064400911431856656901982789948285309956111848686906152664473350940486507451771223435835260168971210087470894448460745593956840586530527915802541450092946574694809584880896601317519794442862977471129319781313161842056501715040555964011899589002863730868679527184420789010551475067862907739054966183120621407246398518098981106431219207697870293412176440482900183550467375190239898455201170831410460483829448603477361305838743852756938687673
e= 3
c= 2205316413931134031074603746928247799030155221252519872649649212867614751848436763801274360463406171277838056821437115883619169702963504606017565783537203207707757768473109845162808575425972525116337319108047893250549462147185741761825125 


def root(n):
    a = 1
    b = n
    while (b-a) > 1:
        mid = (a+b)//2
        if (mid**3)>n:
            b = mid
        else:
            a = mid
        
    if a**3 == n:
        return a
    elif b**3 == n:
        return b
    else:
        return 0

m = root(c)
print (m)
p = hex(m)
print(p)
tex = codecs.decode(p[2:] , 'hex').decode('utf-8')
print(tex)

```
```
13016382529449106065894479374027604750406953699090365388202874238148389207291005
0x7069636f4354467b6e3333645f615f6c41726733725f655f36303663653030347d
picoCTF{n33d_a_lArg3r_e_606ce004}
```


![screenshot]("C:/Users/anant/OneDrive/Pictures/MiniRSA.png")

What you learned through solving this challenge:

1. RSA
2. encoding and decoding
3. Effects of the value of e on a RSA encryption

Other incorrect methods you tried:

- tried to find out the private key using mod n, realised it was supposed to be phi of n and not mod n

References

- stackoverflow.com
- geeksforgeeks.com
