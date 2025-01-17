# Week 3 Exercises

This week’s exercises focus on block ciphers.

*Pages 53-75* from the course book could be helpful for this exercise. It is available in the library of the University of Oulu in [digital format](https://oula.finna.fi/Record/oy_electronic_oy.9917612964306252).

## Environment

You should have access into Linux/Unix environment to be able to complete the final task.

The course virtual machine is suitable.

## Grading

You are eligible for following points from the exercise. Previous task(s) should be completed before going further.

Task #|Grade|Description|
-----|:---:|-----------|
Task 1 | 2 | Modes of operation
Task 2 | 3 | Wrong model type of attack
Task 3 | 4 | Forged cipher
Task 4 | 5 | Padding oracle

## Task 1: Modes of operation

Let's have a practical look at different modes of operations.

**Task 1.1.** Pick a programming language and a crypto library that supports AES.

Take a short message with two identical message blocks (e.g. all zeroes). Notice that AES has a block length of 128 bits.

Generate a suitable key (e.g. 128 bits) to use with AES. 

Encrypt your message using three different modes of operation ECB, CBC and CTR with the same key. Compare the encryptions, from the part of the first and second identical message blocks. Describe the results.

**Task 1.2.** What can you say about for example the indistinguishability properties of the three modes of operation? 

**Task 1.3.** Is there a difference in the overhead of the encrypted messages (i.e. are some messages longer/shorter than the original plaintext)?

> Include source code and answer the questions. You can highlight interesting comparison results with screenshots for example.

## Task 2: Wrong model type of attack

<p align="right">
<img src="img/encryptic.png" alt="Random number. Source: XKCD" height="400px" align="right"/>
</p>


In some cases you can use a very secure cryptographic primitive (in this case a block cipher) but fail to protect the data because the threat model you are using is completely wrong. In this task you will learn more about this type of failure through a real world example.

Familiarize yourself with the Adobe password attack from 2013 [for example from here.](https://arstechnica.com/information-technology/2013/11/how-an-epic-blunder-by-adobe-could-strengthen-hand-of-password-crackers/)

**Task 2.1.** Complete some of the crossword puzzles made using the leaked database and encrypted passwords at https://zed0.co.uk/crossword/. The puzzle's origins lies in the xkcd comic which can seen on the right.

 > Include screen captures of completed puzzle(s) in your work.
 
**Task 2.2.** What is the method used to protect the passwords in the leaked Adobe database? 

**Task 2.3.** What is the “industry standard” for protecting passwords in databases? Method might be totally different in these days.

**Task 2.4.** Why does the mistake allow for easy decryption of the passwords (i.e. making a crossword puzzle)?

**Task 2.5.** The mode of operation chosen in the Adobe case is ECB. Would some other encryption mode of operation have helped? If yes, how? If not, why? If both, then how and why not?


> Answer the questions shortly (3-5 sentences / question). Mention possible sources.


## Task 3: Forged cipher

In this task you will do a similar attack as in Week 1 Task 1, but against a real world secure encryption scheme. The message below is encrypted with AES (a secure standard for symmetric encryption) using a provably secure mode of operation. Yet, you should be able to modify the message according to the task below.

You have managed to intercept the following encrypted message:

`a7896ad1b2f7da8d40b33d1438e04a839a88b5c9a97625fe5017a5e1fb542072595d804d5ad1a3af11ea7244a39d76cde1`

You have information that tells you it is the unauthenticated encryption of the following message: 

`Move the tables to the patio as soon as possible!`

The intelligence also tells you that the encryption is done using AES encryption in Counter mode with a 128 bit key and an unknown (but fixed) initialization vector (IV). They also use plain ASCII encoding of their text before the actual encryption.

**Task 3.1.** Your challenge is to provide a ciphertext that decrypts to:

`Move the chairs to the house as soon as possible!`

Ciphertext should be in similar format than the original one. You can check that you have produced the correct one, comparing it to following sha256 hash:

> `102f853f3e0f38fa7ba7448e6933acaaec5c1bd975c93fc65bff4faa94d2ca34`

**Task 3.2.** What was the flaw here? Are we actually using block cipher here?

**Task 3.3.** What limitations you have on modifying the ciphertext?

> Include possible source code for producing the ciphertext and answer the questions.

## Task 4: Padding oracle

Failed CBC encryption implementation could lead for catastrophic consequences. Implementation fail could be as little as telling when decryption of given ciphertext is successful or not, by checking on if decryption provides plaintext with valid padding.

Take a look at the padding oracle attack in the course book, on the page 74.

You are given a ciphertext and an executable binary as a command-line application which is demonstrating the interface for possible bigger software implementation. Make a padding oracle attack and decrypt the given ciphertext. 

Provided binary uses `AES-128` encryption with `PKCS#7` padding. Initialization vector is in the ciphertext as a prefix.

Binary is named as `decryptor` in the [files](files) folder. It is expected to be executed on glibc enabled Linux environment. Ciphertext is in raw binary format in the same folder.

> Return source code and the decrypted text. Describe shortly, how you could avoid this attack by using different methods.

> If you are using existing tools for making the attack, you **need to write additionally step-by-step** guide, how the attack works in this context; what the tool is doing on your behalf. Include all commands and mention these tools.
