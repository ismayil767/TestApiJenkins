FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build-env
WORKDIR /app

COPY *.csproj .

RUN dotnet restore /app/*.csproj

COPY . ./

RUN dotnet publish --no-restore -c Release -o /app/out 


FROM mcr.microsoft.com/dotnet/runtime:6.0
WORKDIR /app
COPY --from=build-env /app/out .
ENTRYPOINT ["dotnet","TestApiJenkins.dll"]
