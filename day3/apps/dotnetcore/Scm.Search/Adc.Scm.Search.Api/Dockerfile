# Setup environment
FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build

## Setup build space
WORKDIR /app
COPY . ./

## 
#### This is a great place to set up environment information
#### such as versioning, build time etc.
##

## Build app
RUN dotnet publish -o /app/out -c Release ./Adc.Scm.Search.Api.csproj

# Build runtime image
FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS runtime

## Copy build
WORKDIR /app
COPY --from=build /app/out .

# Select non-root port
ENV ASPNETCORE_URLS=http://+:5000

# Do not run as root user
RUN chown -R www-data:www-data /app
USER www-data

# Launch dll
ENTRYPOINT ["dotnet", "Adc.Scm.Search.Api.dll"]