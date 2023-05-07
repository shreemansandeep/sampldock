# Start with the .NET Core 6.0 SDK image
FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build-env

# Set the working directory to /app
WORKDIR /src

# Copy the project file and restore dependencies
COPY sampldock/sampldock.csproj .
RUN dotnet restore

# Copy the remaining source code
COPY . .

# Build the application
RUN dotnet publish -c Release -o  /app

# Start with the .NET Core 6.0 runtime image
FROM mcr.microsoft.com/dotnet/core/aspnet:6.0

# Set the working directory to /app
WORKDIR /app

# Copy the built application from the previous stage
COPY --from=build-env /app .

# Expose port 80
EXPOSE 80

# Start the application
ENTRYPOINT ["dotnet", "sampldock.dll"]
