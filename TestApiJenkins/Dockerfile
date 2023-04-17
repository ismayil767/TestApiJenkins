#FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build-env
#WORKDIR /app
#
#COPY *.csproj .
#
#RUN dotnet restore 
#
#COPY . .
#
#RUN ls
#RUN ls ..
#
#RUN dotnet publish --no-restore -c Release -o out
#
#
#FROM mcr.microsoft.com/dotnet/runtime:6.0
#WORKDIR /app
#COPY --from=build-env /app/out .
#ENTRYPOINT ["dotnet","TestApiJenkins.dll"]
#
FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["TestApiJenkins.csproj", "TestApiJenkins/"]
RUN dotnet restore "TestApiJenkins.csproj"
COPY . .
WORKDIR "/src"
RUN dotnet build "TestApiJenkins.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "TestApiJenkins.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "TestApiJenkins.dll"]