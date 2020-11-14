# Password Audit (60 points)

File(s): 

[password.lst](password.lst) [4 KB]\
[shadow](shadow) [1 KB]

## Question:

Simply concatenate the passwords from the shadow file and submit as the key. Easy!

## Answer:

grannypinkieminutecornered

## Solution:

No surprise here, the solution to this challenge won't be so easy as the challenge claims. In order to solve this problem, we can write a program like the Python code below, to solve this for us:

```py
import subprocess

# Read the passwords file and save them to a list
password_list = open('password.lst', 'r')
passwords = password_list.read().splitlines()
password_list.close()

# Read the shadow file and save each line to a list
shadow_file = open('shadow', 'r')
hashes = shadow_file.read().splitlines()
shadow_file.close()

salts = []

# For each hash in the shadow file...
for index in range(len(hashes)):
    # Split up the parts of the line using the $ symbol as the delimiter
    dollar_splits = hashes[index].split('$')

    # Assign the third part of the line as the salt
    salt = dollar_splits[2]
    salts.append(salt)

    # Assign the first part of the fourth part of the line as the SHA hash
    sha_hash = dollar_splits[3].split(':')[0]
    hashes[index] = sha_hash

# For each salt in the shadow file...
for salt in salts:
    # For each of the possible passwords...
    for password in passwords:
        # Run a command to generate a SHA-512 hash using the given password and salt
        cmd = subprocess.Popen(["mkpasswd", "-m", "sha-512", password, salt], stdout=subprocess.PIPE, stderr=subprocess.STDOUT)
        stdout,stderr = cmd.communicate()
        new_hash = stdout.decode("utf-8")[12:-1]

        # Compare the generated hash to the hash stored in the shadow file
        if new_hash in hashes:
            # If the hashes match, then we've found a password!
            print("$" + salt + "$" + new_hash + " === " + password)
            break
```

Running this program will give us the following output:

```
$UNMfp2ql$WxYqHjbXjM5xPAnXBrwFxbKII0P9QjrfPiLRWyviFF4dTvlcVib/PCQDlhN0TXLhnQIvQpfIjCO3sTeRMme6D0 === granny
$h4SPWV1y$cQtVzk0m3Zxf74cDr9aEB8QUs65QJrkqArxOljgw3jU7dC1NEkJ0w.hfsFm5XcSQ11nyOzJ./Q5Bi7O/Ut45R0 === pinkie
$4Hb7OixZ$qFv0/cQMJn9dL4vgJ46Auri7CYab0dabA2VlExS45bjHa/c4uGnBS2eLIkhoqzqmOVzRwFimT8Wj3zXQ19YW10 === minute
$OysrFFtv$Ph8ZfZkztxRSVhjOYbLXkja641n8rJbaZgoddSAiuSiDjwekbz7HrRztp.o/AeG0UPvaqT.cqRmXYu8xJ66Mp1 === cornered
```

This lists out each salt, hash, and their corresponding cracked password. Putting each of these passwords together, our flag is grannypinkieminutecornered.

| [Previous Challenge](/Challenges/Protect-And-Defend/10/README.md) | [Return to Challenges](/Challenges/../../../#modules) | [Next Challenge](/Challenges/Securely-Provision/1/README.md) |
| :------- | :-----: | ------: |