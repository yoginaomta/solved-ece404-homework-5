Download Link: https://assignmentchef.com/product/solved-ece404-homework-5
<br>
In this homework, you will become familiar with the ANSI X9.31 pseudo-random number generator (PRNG) and the Counter (CTR) mode for using block ciphers.

Both parts will require the use of your AES implementation from homework 4. If for some reason you did not finish homework 4 and are unable to finish your AES implementation by the deadline for homework 5, you may use the implementation found in the PyCryptoDome/PyCrypto package.

<h1>Part 1: X9.31 Pseudo-Random Number Generator</h1>

Section 10.6 of Lecture 10 talks about the ANSI X9.31 cryptographically secure PRNGs. Your task is to implement a more modern version of this PRNG with the following requirements:

<ol>

 <li>Instead of using 3DES for encrypting the 64-bit vectors as indicated in the lecture notes, use your implementation of AES from homework 4 to encrypt 128-bit vectors. By the way, AES is used instead of 3DES in the newer implementations of X9.31.</li>

 <li>Your script needs to define the PRNG function in the following manner:</li>

</ol>

#Arguments:

# v0: 128-bit BitVector object containing the seed value

# dt: 128-bit BitVector object symbolizing the date and time

# key_file: String of file name containing the encryption key (in ASCII) for AES

# totalNum: integer indicating the total number of random numbers to generate

#Function Description

# Uses the arguments with the X9.31 algorithm to generate totalNum random numbers as BitVector objects

#Returns a list of BitVector objects, with each BitVector object representing a random number generated from X9.31

def x931(v0, dt, totalNum, key_file):

<ol start="3">

 <li>For simplicity’s sake in this homework, you can use the same dt vector for each random number generated in a given call.</li>

 <li>Obviously, dt is supposed to contain the date and time. But for testing purposes, you can set it to a predetermined value (hence, dt is a specifiable argument to the x931(…). function).</li>

</ol>

<strong>How Your X9.31 Code Will Be Tested</strong>

Your x931 function will be tested with a script similar to the one below:

import x931 from BitVector import * v0 = BitVector(textstring=’computersecurity’) #v0 will be 128 bits

#As mentioned before, for testing purposes dt is set to a predetermined value dt = BitVector(intVal=99, size=128) listX931 = x931.x931(v0,dt,3,’keyX931.txt’)

#Check if list is correct

print(’{}
{}
{}’.format(int(listX931[0]),int(listX931[1]),int(listX931[2]))

The correct result for the above script (as well as the keyX931.txt file) can be found in the Homework Section of the ECE 404 website.

<h1>Part 2: AES Encryption in Counter Mode</h1>

In Homework 2, the sudden changes in the image of the helicopter allowed you to see the helicopter’s outline even after encrypting the image. To prevent this from happening, implement AES in CTR mode as described in section 9.5.5 of the lecture notes. Use your implementation of AES from homework 4 as a starting point. For testing purposes, you can use a BitVector with the ASCII encoding of the textstring ‘computersecurity’ for the CTR mode initialization vector.

<ol>

 <li>The encryption function should have the following format:</li>

</ol>

#Arguments:

# iv: 128-bit initialization vector

# image_file: input .ppm image file name

<table>

 <tbody>

  <tr>

   <td width="75"></td>

  </tr>

  <tr>

   <td></td>

   <td></td>

  </tr>

 </tbody>

</table>

# out_file: encrypted .ppm image file name

# key_file: String of file name containing encryption key (in ASCII) #Function Descrption:

# Encrypts image_file using CTR mode AES and writes said file to out_file. No required return value.

def ctr_aes_image(iv,image_file=’image.ppm’,out_file=’enc_image.ppm’, key_file=’key.txt’):

<ol start="2">

 <li>For those who are unaware: the above syntax involving the equals sign in the arguments of the function definition indicates <strong>default arguments </strong>for a Python function definition. For example, when calling ctr aes image(…), if no value is specified for the image file argument, the value ’image.ppm’ is used by default (similar logic applies to out file and key file).</li>

 <li>To ensure that the encryption does not take too long, write each block to the output image file as you encrypt it. Do not store the entire encrypted image in a BitVector as you encrypt it (this will cause a slowdown due to the size of the image).</li>

 <li>As in homework 2, the encrypted image should still be a viewable image file and as such should have an image header (though due to the usage of CTR mode encryption the image should be indistinguishable from the original).</li>

</ol>

<strong>How Your CTR AES Code Will Be Tested</strong>

Your ctr aes image function will be tested with a script similar to the one below

from AES_image import ctr_aes_image from BitVector import * iv = BitVector(textstring=’computersecurity’) #iv will be 128 bits ctr_aes_image(iv,’image.ppm’,’enc_image.ppm’,’keyCTR.txt’)

Further testing can be done by comparing your encrypted image with the encrypted image found on the ECE 404 homework page (which is an encrypted version of the helicopter image from homework 2). You can use xxd enc image.ppm | less

to view the encrypted image data in hexadecimal and compare with what the encrypted image your code generates (you can also use the diff command to see if the two images are identical).