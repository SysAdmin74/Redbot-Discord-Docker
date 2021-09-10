FROM mcr.microsoft.com/windows/servercore:1809 as baseimage
RUN @"%SystemRoot%\System32\WindowsPowerShell\v1.0\powershell.exe" -NoProfile -InputFormat None -ExecutionPolicy Bypass -Command "[System.Net.ServicePointManager]::SecurityProtocol = 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))" && SET "PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin"
RUN choco install openjdk11 -y
RUN choco install git -y
RUN choco upgrade git --params "/GitOnlyOnPath /WindowsTerminal" -y
RUN powershell -NoProfile -ExecutionPolicy Bypass -Command \
    Invoke-WebRequest "https://aka.ms/vs/16/release/vs_community.exe" \
    -OutFile "%TEMP%\vs_community.exe" -UseBasicParsing

RUN "%TEMP%\vs_community.exe"  --quiet --wait --norestart --noUpdateInstaller \
    --add Microsoft.VisualStudio.Component.VC.Tools.x86.x64 \
    --add Microsoft.VisualStudio.Component.Windows10SDK.18362
RUN choco install -y --ignore-package-exit-codes=3010 dotnetfx


FROM baseimage
RUN choco install visualstudio2019buildtools --version=16.0.1.0 -y

FROM baseimage
RUN choco upgrade python3 -y --version 3.8.10
RUN choco upgrade adoptopenjdk11jre -y
RUN py -3.8 -m venv "%userprofile%\redenv"
RUN "%userprofile%\redenv\Scripts\activate.bat"
RUN python -m pip install -U pip setuptools wheel
RUN python -m pip install -U Red-DiscordBot
