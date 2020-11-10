# ssless-pip
Guide to pypi (PIP) without ssl.
***
# SSLESS?
Over the last while I've spent my time on an ARM Chromebook, developing different tools to make CrOS more useable.\
Said Chromebook has a 3.10.18 Release kernel, with very little support for SSL/TLS ~ Neither LibreSSL or OpenSSL work successfully on my device\
Leaving me to use other SSL/TLS implementations, such as `gnutls`, MbedTLS, and WolfSSL.\
These all work great! But theres one small issue Python.\
***
# Python-NoSSL
Compiling Python without OpenSSL is as simple as not having OpenSSL installed!\
Only issue is, `pip`'s (pypi) default index url only works with SSL, thus Python without SSL requires the user to either self host a mirror, or not use `pip`\
Well that doesn't work ~ I recently needed to use `pip`, and there's no way I'm selfhosting a mirror, so I went on a search to find a SSL-less (`http` or `fpt`)\
Server to use with `pip`\
***
## Mirrors
The first Mirror I came across was `ftp.belnet.be`, only theres a slight issue, it returns 403 when attempting to access the `/package/` section of the website, making said mirror, useless.\
For while I tired looking on the actual pypi website to see if mirrors actually existed anymore, long story short, the mirrors that did exist for pypi were all taken down!\
A day or so later I came across `mirrors.aliyun.com`, which actually connects, and was recently updated!\
Pefect we have a mirror!.
# `pip.conf`
Below is a config for using `mirrors.aliyun.com` as the index URL.\`

```
$ cat /etc/pip.cong

[global]
index-url = http://mirrors.aliyun.com/pypi/simple
trusted-host = mirrors.aliyun.com
retries = 20
timeout = 10
```
