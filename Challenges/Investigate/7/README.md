# Security Identifier (60 points)

File(s): none

## Description:

In Windows operating systems, a Security Identifier (or SID) can be used to correlate the activities of an individual across systems, even if the person's name is changes. Can you find Jane Smith's SID in the linked Windows image?

This challenge requires tools for memory forensics. One great tool is https://www.volatilityfoundation.org/

[https://vacr.io/XTtEl](https://vacr.io/XTtEl)

### Answer:

S-1-5-21-3357474304-2915131210-3987339850-1000

### Solution:

Ran the following command:

```
grep -ai "profileimagepath" WindowsVista_0401.vmem | grep -ai "s-1-"
```

Among the output, found the SID.

We can confirm that this is her SID by running the following command:

```
grep -ai "S-1-5-21-3357474304-2915131210-3987339850-1000" WindowsVista_0401.vmem
```

and finding the following line in the resulting output:

```
Registry\User\S-1-5-21-3357474304-2915131210-3987339850-1000\Device\HarddiskVolume1\Users\Jane Smith\NTUSER.DAT
```

| [Previous Challenge](/Challenges/Investigate/6) | [Return to Challenges](/Challenges/../../../#modules) | [Next Challenge](/Challenges/Investigate/8) |
| :------- | :-----: | ------: |