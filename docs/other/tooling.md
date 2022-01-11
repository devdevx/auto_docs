# Tooling

## Windows

### WSL 2

#### Installation

````powershell
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
shutdown –r
wsl --set-default-version 2
````

#### Install linux distro subsystem

All distros are here: https://docs.microsoft.com/en-us/windows/wsl/install-manual

````powershell
curl -o ubuntu.appx https://aka.ms/wslubuntu2004
Add-AppxPackage .\ubuntu.appx
````

Go to Start menu, search for the distro an click to set user and password.

#### Commands

List all distros

````powershell
wsl -l -v
````

Set default distro

````powershell
wsl -s Ubuntu-20.04
````

Run default distro in current directory

````powershell
wsl
````

### Docker

#### Installation

Install Docker Desktop for Windows.

#### Configuration

##### General

Enable "Use the WSL 2 base engine"

##### Resources > WSL INTEGRATION

Enable "Enable Integration with mt default WSL distro"

##### Kubernetes

Disable "Enable Kubernetes"

#### Useful info

When using WSL integration, docker create two distros.

````
\\wsl$\docker-desktop
\\wsl$\docker-desktop-data
````

### InstelliJ

#### Plugins

- Indent Rainbow
- Lombok
- Maven Helper
- Rainbow Brackets
- SonarLint
- VisualVM Launcher
- Go
- Rust
- Python
- Key Promoter X
- Kotlin
- Kotlin Fill Class
- Native Debugging Support
- Request Mapper
- RoboPOJOGenerator
- Toml
- OpenAPI (Swagger) Editor
- Detekt

### SDKMAN!

#### Validate prerequisites

```shell
which zip
which unzip
which curl
which tar
which gzip
```

##### Install `zip`

1. Enter [here](https://sourceforge.net/projects/gnuwin32/files/zip/3.0/)
2. Download `zip-3.0-bin.zip` and `bzip2-1.0.5-bin.zip`
3. Extract `zip.exe` and `bzip2.dll` from the bin`folders
4. Copy the files to `C:\Program Files\Git\mingw64\bin`

##### Disable `curl` SSL

```shell
echo "insecure" > ~/.curlrc
```

#### Install

```shell
curl -s "https://get.sdkman.io" | bash
```

#### Common commands

https://sdkman.io/usage

### DBeaver

### SourceTree

### Compass

### Insomnia

### Postman

### Dive



