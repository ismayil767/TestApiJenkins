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


FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS build-env
WORKDIR /app

# Copy the project file and restore dependencies
COPY *.csproj .
RUN dotnet restore

# Copy the rest of the source code and build the application
COPY . .
RUN dotnet publish -c Release -o out

# Create the final image with only the compiled code
FROM mcr.microsoft.com/dotnet/runtime:6.0
WORKDIR /app
COPY --from=build-env /app/out .
ENTRYPOINT ["dotnet", "TestApiJenkins.dll"]