FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY ["docker_linux/docker_linux.csproj", "docker_linux/"]
RUN dotnet restore "docker_linux/docker_linux.csproj"
COPY . .
WORKDIR "/src/docker_linux"
RUN dotnet build "docker_linux.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "docker_linux.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "docker_linux.dll"]