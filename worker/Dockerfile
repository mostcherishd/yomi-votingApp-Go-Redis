# Build stage
FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build

WORKDIR /source

# Copy project file and restore dependencies
COPY *.csproj ./
RUN dotnet restore

# Copy everything else and publish
COPY . ./
RUN dotnet publish -c Release -o /app --no-restore

# Runtime stage
FROM mcr.microsoft.com/dotnet/runtime:7.0

WORKDIR /app

# Copy built app from build stage
COPY --from=build /app ./

# Run the application
ENTRYPOINT ["dotnet", "Worker.dll"]
