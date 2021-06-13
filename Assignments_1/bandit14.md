# Bandit Level x to y Writeup


Author: [Girik Maskara](https://github.com/girik5502)

Problem Page: [bandit14](https://overthewire.org/bandit/bandit14) 

## List of Commands Used
```
ls - list files in a directory
ssh  - OpenSSH SSH client (remote login program)
echo - display a line of text
nc   - arbitrary TCP and UDP connections and listens
```

## Walkthrough
How did you solve this level? Include the complete thought process, even stuff that didn't work. Give explanations wherever necessary.

This question, basically after connecting to bandit14 through a private SSH key in bandit14 , we just had to read out the password from the file  /etc/bandit_pass/bandit14 which I did using the echo command.

## Password

BfMYroe26WYalil77FoDi9qh59eK5xNr

## Bash/Python script to automate the process
```
ssh bandit14@bandit.labs.overthewire.org -p 2220 "nc localhost 30000 < /etc/bandit_pass/bandit14"
```

## Suggested modifications [Optional]
What can you do to make this level more difficult. The inherent idea should be similar.

