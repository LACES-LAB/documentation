---
title: Manage your space on SCOREC machines
---
5 GB of space is given for each user in the home directory and 500 GB is given in the `/lore/your-username` directory. Both the home and lore directories are shared across all SCOREC machines. The home directory is backed up regularly, but the lore directory is not. So, it is recommended to use the lore directory for large files (e.g. installations) and the home directory for small files (e.g. source files you are working on).

### Quick tip for using VSCode on SCOREC machines remotely
VSCode creates a `.vscode-server` directory in your home directory when you connect to a remote machine for the first time. This directory can grow to a large size (e.g. 1 GB) if you use a lot of extensions. So, it is recommended to change the settings _before the first remote connection_ using vscode as follows: (in the json file that opens when you click on the gear icon on the bottom left corner of VSCode)
    
```json
"remote.SSH.serverInstallPath": {
"machine_name1": "/lore/your-username/your-preferred-directory",
"machine_name2": "/lore/your-username/another-or-same-preferred-directory"
}
```
replace `machine_name1` and `machine_name2` with the name of the machine you are using (e.g. `romulus`). This will create the `.vscode-server` directory in the specified location instead of your home directory.

You can also do the same thing on settings UI by searching for `remote.SSH.serverInstallPath` and changing the value for each machine.

### Change Chrome data directory to lore
If you are using Google Chrome on SCOREC machines, you can change the cache directory to lore to save space in your home directory. To do this, run the following command in the terminal:
```bash
mkdir /lore/your-username/path/to/cache/directory
```
change the path to the directory you want to use for cache. Then, run the following command:
**You have to be connected with X11 forwarding to run this command or directly run it on the machine.**
```bash
google-chrome-stable --user-data-dir=/lore/your-username/path/to/cache/directory
```
This will save about half a GB of space in your home directory.
