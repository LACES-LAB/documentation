---
title: Create a config file for ssh to connect to the Lab computers easily
---

1. Create or open a file in the `.ssh` directory in your home directory. For example, you can create a file named `config` in the `.ssh` directory.

2. Add the following lines to the file:

```
Host jumpgate
  HostName jumpgate.scorec.rpi.edu
  User your_username

Host monopoly
  HostName monopoly
  User your_username
  ProxyJump jumpgate

Host aperture01
  HostName jumpgate.scorec.rpi.edu
  User your_username
  ProxyJump jumpgate
  LocalForward 5906 aperture01.scorec.rpi.edu:3389
```
replace `your_username` with your RCS ID or SCOREC username.

3. Save the file.

4. Now, you can connect to the Lab computers using the following commands:

```bash
ssh monopoly
```