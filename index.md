DIRTY COW ATTACK

As a requirement for my Cryptography Course in my 4th year in college, I have attempted a project namely – Dirty COW Attack. The primary aim of my project was to understand how Dirty COW Attack was used to gain root access in Linux by attackers and how to implement it. 
A Dirty COW (Dirty copy-on-write) was discovered by Phil Oester in 2016. It is a computer security vulnerability for the Linux kernel that affects all Linux-based operating systems including Android. It is a local privilege escalation bug that exploits a race condition in the implementation of the copy-on-write mechanism in the kernel's memory-management subsystem.
The first task of my lab exercise was to set up the environment and required tools. Initially. For that I downloaded the virtual box and Ubuntu that was recommended in the lab. 

DIRTY COW ATTACK
Task 1: Modify a Dummy Read-Only File
The objective of this task is was to write to a read-only file using the Dirty COW vulnerability. For this a dummy file was create in the root directory and then I downloaded the cow_attack.c function which contains 3 threads useful to perform the dirty cow attack. After executing this attack the content which is mapped in our read only dummy file is changed with the content provided by the attacker.
 
Figure 1 - In this picture we show task -1 i.e. how to make a read-only folder and then implement the Dirty COW Attack.

Task 2: Modify the Password File to Gain the Root Privilege Now
I launched the attack on a real system file, so we I gain the root privilege. I choose the /etc/passwd file as our target file as recommended by SeedLabs. This file is world-readable, but non-root users cannot modify it. The file contains the user account information, one record for each user. After that I added a new user 'nikkita' and I used this account to turn 'nikkita' into root using Dirty COW attack.

MORE ABOUT DIRTY COW ATTACK 
Impacts:
•	Because of the race condition, with the right timing, a local attacker can exploit the copy-on-write mechanism to turn a read-only mapping of a file into a writable mapping. 
•	A local attacker could use this to gain root privileges.
•	The attack does not leave traces in the system log. 

How does it occur :
The program has three threads:
1.	Main thread - The main thread maps files to memory, finds where the pattern(which we have to change) is, and then creates two threads to exploit the Dirty COW race condition vulnerability in the OS kernel.
2.	Write thread - Since the mapped memory is of COW type, write thread is used to modify the contents in a copy of the mapped memory, which will not cause any change to the original file.
3.	Madvise thread - The madvise thread discards the private copy of the mapped memory, so the page table can point back to the original mapped memory.

Solution :
•	The only perfect cure to this exploit is a patch or running a newer version which is not vulnerable anymore.
•	The safest option is to upgrade the Linux kernel to the latest versions.



