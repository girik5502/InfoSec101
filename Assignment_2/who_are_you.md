# PicoGym Web Exploitation Writeup



Author: [Girik Maskara](https://github.com/girik5502) 

Challenge Page: [Who are you?](http://mercury.picoctf.net:46199/) 

## Walkthrough
The first page we arrive to says only users from picobrowser can have access. So we modify header "User-Agent" value  to picobrowser using burp. 
Then it says that it doesn't trust users form another site so we add Referer modifier with it's value as the link of the website itself.
Next it says about date, so we add "Date" header with it's value as a date in 2018.
Next it talks about tracking so we use a "DNT" header and make it's value to 1.
Next it only accepts people from Sweden so we use header   "X-Forwarded-For" and make its value as an ip address from Sweden.
Finally it wants the language Swedish so we make "Accept-Language:" as sv and get thr flag. 

## Flag
`picoCTF{http_h34d3rs_v3ry_c0Ol_much_w0w_8d5d8d77}`

## Useful resources (if any)

## Suggested modifications [Optional]
What can you do to make this level more difficult. The inherent idea should be similar.
