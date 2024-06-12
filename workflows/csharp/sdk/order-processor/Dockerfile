# Use the official .NET 8 SDK image from the Microsoft Container Registry (MCR)
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build-env

# Set the working directory
WORKDIR /app

# Copy the project file
COPY *.csproj ./

# Restore the packages
RUN dotnet restore

# Copy the rest of the files
COPY . ./

# Build the application
RUN dotnet publish -c Release -o out

# Use the official .NET 8 ASPNET image from the MCR
FROM mcr.microsoft.com/dotnet/aspnet:8.0

# Set the working directory
WORKDIR /app

# Copy the build output from the build-env image
COPY --from=build-env /app/out .

# Set the entry point for the application
ENTRYPOINT ["dotnet", "WorkflowConsoleApp.dll"]