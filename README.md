# Redbot-Discord-Docker
>Docker verison of Redbot-Discord
>For who want to use the Redbot Discord in docker here had provided docker build files for both Windows and Linux platform. Windows version use windows container as base and Linux use linux container.

## Setup the container

### Windows
- Build a docker image from Dockerfile. You can change the base image version that you are going to use for the container, change it as this line in Dockerfile. `mcr.microsoft.com/windows/nanoserver:"Your Version"`

- Execute the build command and name it as the following name for easily recognize 
```
docker build -t redbotdiscord:init
```
- Continue the setup process by running the image that have built above 
```
docker run -it --name RedBotinit redbotdiscord:init powershell
C:\> redbot-setup
C:\> "copy and paste your discord bot token as the setup said"
```

- Save the container changes to the docker image
```
docker commit "Your container ID" redbotdiscord:final
```

---

### Linux (Coming Soon)

## Run it
### Windows
Run the container with the follow command, you can set a nice name for your container.
```
docker run -it --name RedBot redbotdiscord:final "red yourbotname"
```
