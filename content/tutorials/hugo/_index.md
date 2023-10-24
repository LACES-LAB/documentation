---
title: Hugo
description: "Hugo installation"
weight: 1
---

### Install Hugo on Windows

1. Download the latest Hugo binary from [here](https://github.com/gohugoio/hugo/releases) or v0.119 directly from [here](https://github.com/gohugoio/hugo/releases/download/v0.119.0/hugo_0.119.0_windows-amd64.zip).
2. Extract the zip file to a folder of your choice. For example, `C:\Hugo\bin`.
3. Add the path to the Hugo binary to your PATH environment variable. For example, `C:\Hugo\bin`.
4. Search for "Edit the system environment variables" in the Windows search bar.
5. Click on "Environment Variables...".
6. Under "System variables", select "Path" and click "Edit...".
7. Click "New" and add the path to the Hugo binary. For example, `C:\Hugo\bin`.
8. Click "OK" to save the changes.
4. Open a new command prompt and run `hugo version` to verify that Hugo is installed properly.
5. You can now delete the zip file.

### Install Go on Windows (it is required for Hugo)
1. Download the latest Go binary from [here](https://go.dev/doc/install).
2. Run the installer.

### Install Git on Windows (it is required for Hugo)
1. Download the latest Git binary from [https://git-scm.com/download/win](https://git-scm.com/download/win).
2. Run the installer.

### Run Hugo on Windows
1. Open git bash. You can find it in the Windows search bar. **Do not use the Windows command prompt or PowerShell.**
2. Clone the repository: `git clone your-repository-url`.
3. Navigate to the repository: `cd your-repository-name`.
4. Run Hugo: `hugo server`.
5. Copy the URL from the output and paste it in your browser.

