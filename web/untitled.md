# Recon

## Directories Enumeration

### Dirb

```text
dirb https://10.10.10.100/ /usr/share/wordlists/enum.txt
dirb https://10.10.10.100/ /usr/share/wordlists/enum.txt -X .html,.py,.php
```

### Dirbuster

```text
dirbuster -u https://10.10.10.100/
```

### Gobuster

> dir         Uses dir/file bruteforcing mode  
> dns       Uses DNS subdomain bruteforcing mode  
> vhost    Uses VHOST bruteforcing mode  
>   
> -z, --noprogress        Don't display progress   
> -o, --output string     Output file to write results to \(defaults to stdout\)   
> -q, --quiet                   Don't print the banner and other noise   
> -t, --threads int          Number of concurrent threads \(default 10\)   
> -v, --verbose              Verbose output \(errors\)  
> -w, --wordlist string  Path to the wordlist

```text
gobuster dir -u http://10.10.10.100/ -w /usr/share/wordlists/enum.txt
gobuster dir -u https://10.10.10.100/ -w /usr/share/wordlist/enum.txt -k
```

{% hint style="warning" %}
Error: error on running goubster: unable to connect to https://websitetobf invalid certificate: x509: certificate signed by unknown authority  
**--&gt; Use the -k flag to ignore it**
{% endhint %}

### Wfuzz





