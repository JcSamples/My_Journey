
## ANALYZE EMAIL

Analyze the Header  
Check for Spelling Errors  
Analyze incorrect symbols, such as the Euro or Dollar symbol before or after the value.

Download the Phishing Email and Open it in  
Sublime or another Text Editor

Search for the Sender and check the Reverse DNS

## LINK ARTIFACTS

Next, check for artifacts (links to other sites)  
Simply search in the Text Editor for HTTP or HTTPS and verify `href`  
NOTE: In the example `<a href=3D ...>`, the initial `a` indicates that it is a malicious link.

## FILE ARTIFACTS

==Never open the file==


````powershell
get-filehash --algorithm MD5 , .\"filename.pdf"; get-filehash --algorithm SHA-1 , .\"filename.pdf"
`````
