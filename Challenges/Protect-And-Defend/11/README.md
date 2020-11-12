# Password Audit (60 points)

File(s): 

[password.lst](password.lst)
[shadow](shadow)

## Question:

Simply concatenate the passwords from the shadow file and submit as the key. Easy!

### Answer:

grannypinkieminutecornered

### Solution:

```py
import subprocess

password_list = open('password.lst', 'r')
passwords = password_list.read().splitlines()
password_list.close()

shadow_file = open('shadow', 'r')
hashes = shadow_file.read().splitlines()
shadow_file.close()

salts = []

for index in range(len(hashes)):
    dollar_splits = hashes[index].split('$')

    salt = dollar_splits[2]
    salts.append(salt)

    sha_hash = dollar_splits[3].split(':')[0]
    hashes[index] = sha_hash


for salt in salts:
    for password in passwords:
        cmd = subprocess.Popen(["mkpasswd", "-m", "sha-512", password, salt], stdout=subprocess.PIPE, stderr=subprocess.STDOUT)
        stdout,stderr = cmd.communicate()
        new_hash = stdout.decode("utf-8")[12:-1]

        if new_hash in hashes:
            print("$" + salt + "$" + new_hash + " === " + password)
            break
```

The output is:

```
$UNMfp2ql$WxYqHjbXjM5xPAnXBrwFxbKII0P9QjrfPiLRWyviFF4dTvlcVib/PCQDlhN0TXLhnQIvQpfIjCO3sTeRMme6D0 === granny
$h4SPWV1y$cQtVzk0m3Zxf74cDr9aEB8QUs65QJrkqArxOljgw3jU7dC1NEkJ0w.hfsFm5XcSQ11nyOzJ./Q5Bi7O/Ut45R0 === pinkie
$4Hb7OixZ$qFv0/cQMJn9dL4vgJ46Auri7CYab0dabA2VlExS45bjHa/c4uGnBS2eLIkhoqzqmOVzRwFimT8Wj3zXQ19YW10 === minute
$OysrFFtv$Ph8ZfZkztxRSVhjOYbLXkja641n8rJbaZgoddSAiuSiDjwekbz7HrRztp.o/AeG0UPvaqT.cqRmXYu8xJ66Mp1 === cornered
```


| [Previous Challenge](/Challenges/Protect-And-Defend/10) | [Return to Challenges](/Challenges/../../../#modules) | [Next Challenge](/Challenges/Securely-Provision/1) |
| :------- | :-----: | ------: |