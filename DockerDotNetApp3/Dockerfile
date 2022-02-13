#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build
WORKDIR /src
COPY ["DockerDotNetApp3/DockerDotNetApp3.csproj", "DockerDotNetApp3/"]
RUN dotnet restore "DockerDotNetApp3/DockerDotNetApp3.csproj"
COPY . .
WORKDIR "/src/DockerDotNetApp3"
RUN dotnet build "DockerDotNetApp3.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "DockerDotNetApp3.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "DockerDotNetApp3.dll"]