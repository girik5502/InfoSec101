# MicroCTF Writeup


Author: [Girik Maskara](https://github.com/girik5502) 

Level: Cusco

## Walkthrough
Inspecting the login function we can see that we can’t access the `unlock_door` function as it is always jumped over.

```
4524:  0f93           tst	r15
4526:  0524           jz	#0x4532 <login+0x32>
4528:  b012 4644      call	#0x4446 <unlock_door>
452c:  3f40 d144      mov	#0x44d1 "Access granted.", r15
4530:  023c           jmp	#0x4536 <login+0x36>
```
the code says not to enter a password more than 16 bytes, but it takes input of 48 bytes
as in this line.
```4514:  3e40 3000      mov	#0x30, r14```
so lets try to enter a v big password and upin running we find that the disassembly was 
Over written.
So may possibly override the `login` function 'returns' the `unlock_door` function.
To accomplish this we need to know where the stack pointer when the return statement is being executed.
so we break at the line `453e:  3041           ret` 
and then we observe the sp 
`sp  43fe`
then looking at the memory dump.
```
43e0:   5645 0300 ca45 0000 0a00 0000 3a45 5050   VE...E......:EPP
43f0:   5050 5050 5050 5050 5050 5050 5050 4644   PPPPPPPPPPPPPPFD
4400:   0040 0044 1542 5c01 75f3 35d0 085a 3f40   .@.D.B\.u.5..Z?@
```
So we see that at the offset 0x11 we need to enter the memory address `4446` keeping in mind that it is little endian.

So the final payload must be `101010101010101010101010101010104644` which should unlock the door.

## Password
`101010101010101010101010101010104644`

