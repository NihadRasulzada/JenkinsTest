# Build stage
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build-env
WORKDIR /app

# Proje dosyalarını kopyala ve restore et
COPY *.csproj ./
RUN dotnet restore

# Tüm kaynak dosyalarını kopyala ve yayınla
COPY . ./
RUN dotnet publish -c Release -o out --no-restore

# Run stage
FROM mcr.microsoft.com/dotnet/aspnet:8.0
WORKDIR /app
COPY --from=build-env /app/out .

ENTRYPOINT ["dotnet", "Test.Api.dll"]
