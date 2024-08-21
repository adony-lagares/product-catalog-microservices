# Estágio base
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
WORKDIR /app
EXPOSE 80

# Estágio de build
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY ["ConfigServer/ConfigServer.csproj", "ConfigServer/"]
RUN dotnet restore "ConfigServer/ConfigServer.csproj"
COPY . .
WORKDIR "/src/ConfigServer"
RUN dotnet build "ConfigServer.csproj" -c Release -o /app/build

# Estágio de publicação
FROM build AS publish
RUN dotnet publish "ConfigServer.csproj" -c Release -o /app/publish

# Estágio final
FROM base AS final
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "ConfigServer.dll"]
