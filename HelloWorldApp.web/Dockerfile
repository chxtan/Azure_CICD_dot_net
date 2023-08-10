# Use the official .NET SDK image as the base image
FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build

# Set the working directory in the container
WORKDIR /app

# Copy the project file to the container
COPY *.csproj ./

# Restore the dependencies
RUN dotnet restore

# Copy the remaining files to the container
COPY . ./

# Build the application
RUN dotnet publish -c Release -o out

# Create a new image for the runtime
FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS runtime

# Set the working directory in the container
WORKDIR /app

# Copy the published output from the build image to the runtime image
COPY --from=build /app/out .

# Expose port 80 for the web application
EXPOSE 80

# Start the application
ENTRYPOINT ["dotnet", "YourAppName.dll"]
