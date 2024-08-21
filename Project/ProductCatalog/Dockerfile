# Estágio base
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
WORKDIR /app
EXPOSE 80

# Estágio de build
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY ["ProductCatalog/ProductCatalog.csproj", "ProductCatalog/"]
RUN dotnet restore "ProductCatalog/ProductCatalog.csproj"
COPY . .
WORKDIR "/src/ProductCatalog"
RUN dotnet build "ProductCatalog.csproj" -c Release -o /app/build

# Estágio de publicação
FROM build AS publish
RUN dotnet publish "ProductCatalog.csproj" -c Release -o /app/publish

# Estágio final
FROM base AS final
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "ProductCatalog.dll"]
