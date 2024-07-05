

mcr.microsoft.com/dotnet/framework/aspnet:4.8-windowsservercore-ltsc2019
mcr.microsoft.com/dotnet/framework/runtime:4.8-windowsservercore-ltsc2019
mcr.microsoft.com/dotnet/framework/sdk:4.8-windowsservercore-ltsc2019

mcr.microsoft.com/windows/nanoserver:1809
mcr.microsoft.com/windows/servercore:ltsc2019

# https://learn.microsoft.com//virtualization/windowscontainers/quick-start/set-up-environment



# https://hub.docker.com/_/microsoft-dotnet
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /source

# copy csproj and restore as distinct layers
COPY *.sln .
COPY aspnetapp/*.csproj ./aspnetapp/
RUN dotnet restore

# copy everything else and build app
COPY aspnetapp/. ./aspnetapp/
WORKDIR /source/aspnetapp
RUN dotnet publish -c release -o /app --no-restore

# final stage/image
FROM mcr.microsoft.com/dotnet/aspnet:8.0
WORKDIR /app
COPY --from=build /app ./
ENTRYPOINT ["dotnet", "aspnetapp.dll"]
