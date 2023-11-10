---
title: Connect to Aperture
---

1. Add the following lines to the `config` file in the `.ssh` directory in your home directory:
```bash
Host aperture01
  HostName jumpgate.scorec.rpi.edu
  User your_username
  ProxyJump jumpgate
  LocalForward 5906 aperture01.scorec.rpi.edu:3389
```
replace `your_username` with your RCS ID.

2. Open a terminal window on your computer. On Windows, you can use the Git Bash terminal that comes with Git for Windows. On Mac, you can use the Terminal application. On Linux, you can use the terminal application that comes with your distribution.

3. Type the following command in the terminal window:
```bash
ssh -X aperture01
```

4. When prompted, enter your RCS ID password. Or you can set up ssh on lab computers for passwordless login to the Lab computers.

5. Search for `Remote Desktop Connection` in the start menu and open it.

6. In the `Remote Desktop Connection` window, type `localhost:5906` in the `Computer` field and click `Connect`.

7. When prompted, enter your RCS ID password. Or you can set up ssh on lab computers for passwordless login to the Lab computers.

8. You will be connected to the Aperture computer. You can now use the computer as if you are sitting in front of it.