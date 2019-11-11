# Sitecore docker demo sxa

Docker can help us to to easily spin up Sitecore versions, keep your project isolated, and speed up build and development time.
The Sitecore docker images repository contain Dockerfiles to create base images for each version and role of Sitecore. 
In the docker registry are built images which also contain our partner license.  The images are built every week to keep up with updated base images such as Window server core releases.

# Prerequisities
For using Sitecore with docker you will need:
•	Windows 10 1809 (or later)
•	Docker for Windows 18.09.2 (or later)
•	Your Sitecore partner license

# Initial configuration

You will need to configure the shared docker registry, so you will need the Azure CLI and authenticate.
You will need to provide your license file as it is not included in the docker image itself (and we have different licenses for different offices and one registry). The Sitecore docker images repository samples expects that you either have your license file in c:\license, or define the environment variable LICENSE_PATH. Similar by defining the environment variable REGISTRY pointing to our registry, you can use the samples directly.
We recommend that you define those variables on your workstation to simplify setting up new solutions:
Initial configuration with powershell 

# Azure CLI
Invoke-WebRequest -Uri https://aka.ms/installazurecliwindows -OutFile .\AzureCLI.msi; Start-Process msiexec.exe -Wait -ArgumentList '/I AzureCLI.msi /quiet' ; 
az login

# Set env var for shared docker registry
[System.Environment]::SetEnvironmentVariable("REGISTRY", "x.azurecr.io/", "Machine")

# Set env var for Sitecore license file. Make sure that the path exists and you have your license in there

[System.Environment]::SetEnvironmentVariable("LICENSE_PATH", "${env:USERPROFILE}\Dropbox (x)\<country specific>\<directory with Sitecore license>", "Machine")

# Reload environment variables (or restart the powershell sesssion)
refreshenv
Environment variables can be used in docker-compose files, if the variable is defined it will be used, otherwise it will look for a local .env file with the variables variables.
