FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build-env
WORKDIR /app

COPY *.csproj .

RUN dotnet restore

COPY . ./

RUN dotnet publish --no-restore -c Release -o dist 


FROM mcr.microsoft.com/dotnet/runtime:6.0
WORKDIR /app
COPY --from=build-env /app/dist .
ENTRYPOINT ["dotnet","TestApiJenkins.dll"]
