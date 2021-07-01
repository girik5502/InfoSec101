# MicroCTF Writeup


Author: [Girik Maskara](https://github.com/girik5502) 

Level: Hanoi

## Walkthrough
Inspecting main function, it just calls the function login so let's inspect that.
```
4520 <login>
4520:  c243 1024      mov.b	#0x0, &0x2410
4524:  3f40 7e44      mov	#0x447e "Enter the password to continue.", r15
4528:  b012 de45      call	#0x45de <puts>
452c:  3f40 9e44      mov	#0x449e "Remember: passwords are between 8 and 16 characters.", r15
4530:  b012 de45      call	#0x45de <puts>
4534:  3e40 1c00      mov	#0x1c, r14
4538:  3f40 0024      mov	#0x2400, r15
453c:  b012 ce45      call	#0x45ce <getsn>
4540:  3f40 0024      mov	#0x2400, r15
4544:  b012 5444      call	#0x4454 <test_password_valid>
4548:  0f93           tst	r15
454a:  0324           jz	$+0x8
454c:  f240 4700 1024 mov.b	#0x47, &0x2410
4552:  3f40 d344      mov	#0x44d3 "Testing if password is valid.", r15
4556:  b012 de45      call	#0x45de <puts>
455a:  f290 5400 1024 cmp.b	#0xa9, &0x2410
4560:  0720           jne	#0x4570 <login+0x50>
4562:  3f40 f144      mov	#0x44f1 "Access granted.", r15
4566:  b012 de45      call	#0x45de <puts>
456a:  b012 4844      call	#0x4448 <unlock_door>
456e:  3041           ret
4570:  3f40 0145      mov	#0x4501 "That password is not correct.", r15
4574:  b012 de45      call	#0x45de <puts>
4578:  3041           ret
```
On observing we can directly see that to open the unlock_door 
function we need the condition `455a:  f290 5400 1024 cmp.b	#0xa9, &0x2410` to 
be true.
the password starts storing at the memory address `#0x2400`.
we need the byte at address `#0x2410` as ‘9a’.
So we add 16 random characters followed by the ‘9a’ in the payload , in hex mode.
`101010101010101010101010101010109a`
## Password
`101010101010101010101010101010109a`

