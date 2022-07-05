### Go to this page 🥭

#### Links:

[Install .NET on Linux](https://docs.microsoft.com/en-us/dotnet/core/install/linux)

[How to check that .NET is already installed](https://docs.microsoft.com/en-us/dotnet/core/install/how-to-detect-installed-versions?pivots=os-linux)

[How to Install Dotnet Core on Ubuntu 20.04](https://tecadmin.net/how-to-install-net-core-on-ubuntu-20-04/)

<br>
<br>

---

<br>
<br>

## [How to Install Dotnet Core on Ubuntu 20.04](https://tecadmin.net/how-to-install-net-core-on-ubuntu-20-04/)

<br>

- check this video mn: 13:41 [How to install Unity 2020 on a Ubuntu Linux - Step by Step guide - .Net SDK + Mono + VS Code](https://youtu.be/ACo03HTwGiU)

<br>

## Step 1 – Enable Microsoft PPA

#### Paste this in your console (desktop is fine)

```javascript
// 0  Copy the whole line below until deb
sudo wget https://packages.microsoft.com/config/ubuntu/20.04/packages-microsoft-prod.deb
//
// 1
sudo dpkg -i packages-microsoft-prod.deb

```

<br>
<br>

### Step 2 – Installing Dotnet Core SDK

> .NET Core SDK is the Software development kit used for developing applications. If you are going to create a application or making changes to existing application, you will required .net core sdk package on your system.

- You can copy the 3 lines and paste it directly, I paste them 1 by 1 ✋

<br>

###### To install .NET Core SDK on Ubuntu 20.04 LTS system, execute the commands:

```javascript
sudo apt update
sudo apt install apt-transport-https
sudo apt install dotnet-sdk-3.1
```

<br>

#### After that, test if it worked:

- type this: **dotnet** in your console

<br>

##### Result ✋

- it worked

```javascript
$ dotnet

Usage: dotnet [options]
Usage: dotnet [path-to-application]

Options:
  -h|--help         Display help.
  --info            Display .NET information.
  --list-sdks       Display the installed SDKs.
  --list-runtimes   Display the installed runtimes.

path-to-application:
  The path to an application .dll file to execute.

```
