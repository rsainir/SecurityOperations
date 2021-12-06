# The Challenge [Reconaissance]

Sometimes, routers can break packets up into fragments to meet abnormal networking requirements, and the endpoint will be responsible for putting these back together. Sometimes however, this doesn't go as planned, as Microsoft found out with CVE-2021-24074. We'd like to see the function responsible for this vulnerability, but we're having some trouble finding its name... Could you see if you could find it?

# Solution

This one takes a little bit of digging to find some sample POCs for this CVE. 

The official Microsoft disclosure of this vuln showed the shell commands via netsh to circumvent the vulnerability, but did not show a POC or way to exploit.

Looking for a POC in AttackerKB for CVE-2021-24074 gives similar information, as well as some ATT&CK TTPs. Most importantly, looking through the posts by users for the Analysis, we find a link to a POC https://doar-e.github.io/blog/2021/04/15/reverse-engineering-tcpipsys-mechanics-of-a-packet-of-the-death-cve-2021-24086/#bonus-cve-2021-24074

Looking through this reverse-engineer's Python exploit, we see the following snippet:

``` Snippet:
      __int16 __fastcall Ipv4pReceiveRoutingHeader(Packet_t *Packet)
      {
        // ...
        // kd> db @rax
        // ffffdc07`ff209170  ff ff 04 00 61 62 63 00-54 24 30 48 89 14 01 48  ....abc.T$0H...H
        RoutingHeaderFirst = NdisGetDataBuffer(FirstNetBuffer, Packet->RoutingHeaderOptionLength, &v50[0].qw2, 1u, 0);
        NetioAdvanceNetBufferList(NetBufferList, v8);
        OptionLenFirst = RoutingHeaderFirst[1];
        LenghtOptionFirstMinusOne = (unsigned int)(unsigned __int8)RoutingHeaderFirst[2] - 1;
        RoutingOptionOffset = LOBYTE(Packet->RoutingOptionOffset);
        if (OptionLenFirst < 7u ||
          LenghtOptionFirstMinusOne > OptionLenFirst - sizeof(IN_ADDR))
        {
          // ...
          goto Bail_0;
        }
```

The above function **Ipv4pReceiveRoutingHeader** is the centerpiece of this POC, and indeed the flag is **MetaCTF{Ipv4pReceiveRoutingHeader}**
        

