# Local installation Basic system

We just provide the basic system setup for a Windows 10 environment for other OS like Linux or
Mac please use you own creativity to install the same components.

## Window Subsystem Linux 2

```Powershell
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
```

Restart your machine! Download and run this to and install the
[WSL2-Linux-kernel-update-package](https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi)
for x64 machines

```Powershell
wsl --set-default-version 2
```

From the “Microsoft store” search and install Ubuntu LTS 20.04. From within the Ubuntu environment
run your updates.

```bash
sudo apt-get update
sudo apt-get upgrade
```

## Docker desktop

See also: - <https://docs.docker.com/docker-for-windows/wsl/>

Download and install
[Dockerdesktop](https://hub.docker.com/editions/community/docker-ce-desktop-windows/)

Upon installation enable WSL 2 or from From the Docker menu, select

* Settings > General >[Select] Use the WSL 2 based engine.

Restart Docker Desktop and go to

* Settings > Resources > WSL Integration. >[Select] Ubuntu-20.04 [Apply & Restart]

## Install Netbox

```powershell
git clone -b release https://github.com/netbox-community/netbox-docker.git
cd netbox-docker
$override_yml= @"
version: '3.4'
services:
  netbox:
    ports:
      - 8000:8080
"@
Set-Content ".\docker-compose.override.yml" $override_yml

docker-compose pull
docker-compose up -d
```

<http://127.0.0.1:8000/> or <http://localhost:8000/>
login_user: admin
login_password: netbox or admin

or for local AWX for example use

<http://[your-local-ip]:8000>

> NOTE: Netbox Documentation [here](https://github.com/netbox-community/netbox-docker#quickstart)
