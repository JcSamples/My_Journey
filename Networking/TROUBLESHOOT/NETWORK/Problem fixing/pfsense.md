![](Pasted%20image%2020240616131125.png)

### Check if pfSense Resolves Domain Names

![](Pasted%20image%2020240616131417.png)

Or Select Option 13 in pfSense



### Error while fetching package

If it doesn't work in the Web Browser:

![](Pasted%20image%2020240616132819.png)
![](Pasted%20image%2020240616132908.png)

````shell
pfSense-repoc
pkg-static -d update
pkg-static install -fy pkg pfSense-repo pfSense-upgrade
`````


If this also doesn’t work, there might have been an error during installation (perform a new installation).