# The Challenge [Forensics]

Window Pains 4
Category Points

Details
We want to see if any other machines are infected with this malware. Using the memory dump file from Window Pains, submit the SHA1 checksum of the malicious process.

Submit the flag as flag{SHA1 hash}.

CAUTION: Practice good cyber hygiene! Use an isolated VM to download/run the malicious process. While the malicious process is relatively benign, if you're using an insecurely-configured Windows host, it may be possible for someone to compromise your machine if they can reach you on the same network.


# Solution
Making sure Volatility 3 is downloaded and installed on machine, for this challenge we had volatility3 as a PATH variable in Kali.
In a Kali linux VM, we can grab the memory dump for the process with the PID 8180 from the previous Challenge (was completed by another team member, but worked on by many of us) in volatility using;
```shell
> vol.py -f physmemraw windows.pslist.PsList --pid 8180 --dump
> sha1sum ./file...userinit.exe.img

962d96f30c8f126cbcdee6eecc5e50c3a408402b

```

After dumping the file of the target process, we check the SHA1Sum and  get our flag: flag{962d96f30c8f126cbcdee6eecc5e50c3a408402b}
