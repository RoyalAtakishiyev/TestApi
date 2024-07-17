# Use the official .NET Core SDK image for the build process
FROM mcr.microsoft.com/dotnet/core/sdk:3.1 AS build-env
WORKDIR /app
# Copy the csproj file(s) and restore dependencies
COPY *.csproj ./
RUN dotnet restore
# Copy the rest of the files and build the project
COPY . ./
RUN dotnet publish -c Release -o out
# Use the official .NET Core runtime image for running the application
FROM mcr.microsoft.com/dotnet/core/aspnet:3.1
WORKDIR /app
COPY --from=build-env /app/out .
ENTRYPOINT ["dotnet", "Api.dll"]
