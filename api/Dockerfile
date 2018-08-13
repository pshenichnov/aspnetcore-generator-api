# Build Stage
#FROM microsoft/aspnetcore-build:2 AS build-env
FROM microsoft/dotnet:2.1.302-sdk AS build-env
WORKDIR /api

COPY api.csproj .
RUN dotnet restore

COPY . .
RUN dotnet publish -o /publish

# Runtime Image Stage
#FROM microsoft/aspnetcore:2
FROM microsoft/dotnet:2.1.2-aspnetcore-runtime
WORKDIR /publish
COPY --from=build-env /publish .
ENTRYPOINT ["dotnet", "api.dll"]