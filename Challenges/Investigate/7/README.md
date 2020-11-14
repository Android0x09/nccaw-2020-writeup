# Security Identifier (60 points)

File(s): [WindowsVista_0401.vmem](https://vacr.io/XTtEl) [524,288 KB]

## Question:

In Windows operating systems, a Security Identifier (or SID) can be used to correlate the activities of an individual across systems, even if the person's name changes. Can you find Jane Smith's SID in the linked Windows image?

This challenge requires tools for memory forensics. One great tool is [Volatility](https://www.volatilityfoundation.org/).

[https://vacr.io/XTtEl](https://vacr.io/XTtEl)

## Answer:

S-1-5-21-3357474304-2915131210-3987339850-1000

## Solution:

First, we can download the Windows image from the link provided. Depending on your Internet connection, this may take a little while to complete.

Next, we can open up a Linux terminal using either [WSL](https://docs.microsoft.com/en-us/windows/wsl/install-win10) or a [Linux VM](https://www.linuxvmimages.com/) and run the following command:

```
grep -ai "profileimagepath" WindowsVista_0401.vmem | grep -ai "s-1-"
```

Among the output, we can find a user's SID.

We can confirm that this SID belongs to the user we're interested in by running the following command using the discovered SID as a search term:

```
grep -ai "S-1-5-21-3357474304-2915131210-3987339850-1000" WindowsVista_0401.vmem
```

We can then look through the resulting output and find the following line which confirms that the SID belongs to Jane Smith:

```
Registry\User\S-1-5-21-3357474304-2915131210-3987339850-1000\Device\HarddiskVolume1\Users\Jane Smith\NTUSER.DAT
```

| [Previous Challenge](/Challenges/Investigate/6/README.md#question) | [Return to Challenges](/Challenges/../../../#modules) | [Next Challenge](/Challenges/Investigate/8/README.md#question) |
| :------- | :-----: | ------: |