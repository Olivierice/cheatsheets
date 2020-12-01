# Recon

## Directories Enumeration

### Dirb

### Gobuster

### Wfuzz

{% tabs %}
{% tab title="Dirb" %}
I like to use dirb because is pretty straighforward to used as you can see below.

```bash
dirb https://10.10.10.100/ /usr/share/wordlists/enum.txt
dirb https://10.10.10.100/ /usr/share/wordlists/enum.txt -X .html,.py,.php
```

`-a  : Specify your custom USER_AGENT.   
-b : Use path as is.   
-c  : Set a cookie for the HTTP request.   
-E  : path to the client certificate.   
-f : Fine tunning of NOT_FOUND (404) detection.   
-H  : Add a custom header to the HTTP request.   
-i : Use case-insensitive search.   
-l : Print "Location" header when found.   
-N : Ignore responses with this HTTP code.   
-o  : Save output to disk.   
-p  : Use this proxy. (Default port is 1080)   
-P  : Proxy Authentication.   
-r : Don't search recursively.   
-R : Interactive recursion. (Asks for each directory)   
-S : Silent Mode. Don't show tested words. (For dumb terminals)   
-t : Don't force an ending '/' on URLs.   
-u  : HTTP Authentication.   
-v : Show also NOT_FOUND pages.   
-w : Don't stop on WARNING messages.   
-X  / -x  : Append each word with this extensions. -  
z  : Add a milliseconds delay to not cause excessive Flood.`

### Official Documentation

[http://dirb.sourceforge.net/](http://dirb.sourceforge.net/)
{% endtab %}

{% tab title="Gobuster" %}
Gobuster can be used in three different modes:

`dir Uses dir/file bruteforcing mode   
dns Uses DNS subdomain bruteforcing mode   
vhost Uses VHOST bruteforcing mode`

```bash
gobuster dir -u http://10.10.10.100/ -w /usr/share/wordlists/enum.txt
gobuster dir -u https://10.10.10.100/ -w /usr/share/wordlist/enum.txt -k
```

`-z, --noprogress Don't display progress   
-o, --output string Output file to write results to (defaults to stdout)   
-q, --quiet Don't print the banner and other noise   
-t, --threads int Number of concurrent threads (default 10)   
-v, --verbose Verbose output (errors)   
-w, --wordlist string Path to the wordlist`

{% hint style="warning" %}
Error: error on running goubster: unable to connect to https://websitetobf invalid certificate: x509: certificate signed by unknown authority  
**--&gt; Use the -k flag to ignore it.**
{% endhint %}

### Official Documentation

[https://github.com/OJ/gobuster](https://github.com/OJ/gobuster)
{% endtab %}

{% tab title="Wfuzz" %}
Wfuzz is a little bit more complex to use but offers several features, including one that allows to fuzz by knowing the filename but not the intermediate directories.

```bash
wfuzz -c -w dirb/common.txt --hc 404,502 https://target/FUZZ
wfuzz -c -z file,/wordlists/fuzz.txt -z file,/usr/share/wordlists/fuzz2.txt --hc 404 http://target/FUZZ/FUZ2Z
wfuzz -c -w dirb/common.txt --hc 404,502 https://target/FUZZ/index.html
```

`-c    :Output with color  
-v    :Verbose information  
-f filename,printer: :Store results in the output file using the specified printer  
-t N : Specify the number of concurrent connections (10 default)   
-s N : Specify time delay between requests (0 default)   
-R depth : Recursive path discovery being depth the maximum recursion level.   
-D depth : Maximum link depth level.   
-L,--follow : Follow HTTP redirections   
-u url : Specify a URL for the request.   
-z payload : Specify a payload for each FUZZ keyword used in the form of name[,parameter][,encoder]. A list of encoders can be used, ie. md5-sha1. Encoders can be chained, ie. md5@sha1. Encoders category can be used. ie. url Use help as a payload to show payload plugin's details (you can filter using --slice)   
-w wordlist : Specify a wordlist file (alias for -z file,wordlist).   
--hc/hl/hw/hh N[,N]+ : Hide responses with the specified code/lines/words/chars (Use BBB for taking values from baseline)`

Don't forget to use the --help page to see all options!

{% hint style="info" %}
You can add all exceptions you don't want to see behind --hc flag.  
--hc 429,502,404
{% endhint %}

{% hint style="warning" %}
/usr/local/lib/python3.8/dist-packages/wfuzz/**init**.py:34: UserWarning:Pycurl is not compiled against Openssl. Wfuzz might not work correctly when fuzzing SSL sites. Check Wfuzz's documentation for more information.

[https://stackoverflow.com/questions/55929011/pycurl-is-not-compiled-against-openssl-when-i-trie-to-use-wfuzz-how-to-solve-th](https://stackoverflow.com/questions/55929011/pycurl-is-not-compiled-against-openssl-when-i-trie-to-use-wfuzz-how-to-solve-th)
{% endhint %}

### Official Documentation

[https://wfuzz.readthedocs.io/en/latest/index.html](https://wfuzz.readthedocs.io/en/latest/index.html)
{% endtab %}

{% tab title="Final Recon" %}
Final Recon offers several options as Wfuzz does, and it's pretty simple to use.

```bash
finalrecon --dir -s -w /usr/share/wordlists/dirb/common.txt https://target
```

`--headers Header Information   
--sslinfo SSL Certificate Information   
--whois Whois Lookup   
--crawl Crawl Target   
--dns DNS Enumeration   
--sub Sub-Domain Enumeration   
--trace Traceroute   
--dir Directory Search   
--ps Fast Port Scan   
--full Full Recon   
Extra Options:   
-t T Number of Threads [ Default : 30 ]   
-T T Request Timeout [ Default : 30.0 ]   
-w W Path to Wordlist [ Default : wordlists/dirb_common.txt ]   
-r Allow Redirect [ Default : False ]   
-s Toggle SSL Verification [ Default : True ]   
-sp SP Specify SSL Port [ Default : 443 ]   
-d D Custom DNS Servers [ Default : 1.1.1.1 ]   
-e E File Extensions [ Example : txt, xml, php ]   
-m M Traceroute Mode [ Default : UDP ] [ Available : TCP, ICMP ]   
-p P Port for Traceroute [ Default : 80 / 33434 ]   
-tt TT Traceroute Timeout [ Default : 1.0 ]   
-o O Export Output [ Default : txt ] [ Available : xml, csv ]`
{% endtab %}
{% endtabs %}

























