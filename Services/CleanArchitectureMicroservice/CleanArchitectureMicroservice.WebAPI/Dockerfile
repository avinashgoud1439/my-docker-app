##See https://aka.ms/customizecontainer to learn how to customize your debug container and how Visual Studio uses this Dockerfile to build your images for faster debugging.
#
#FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
#USER app
#WORKDIR /app
#EXPOSE 8080
#
#FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
#ARG BUILD_CONFIGURATION=Release
#WORKDIR /src
#COPY ["Services/CleanArchitectureMicroservice/CleanArchitectureMicroservice.WebAPI/CleanArchitectureMicroservice.WebAPI.csproj", "Services/CleanArchitectureMicroservice/CleanArchitectureMicroservice.WebAPI/"]
#RUN dotnet restore "./Services/CleanArchitectureMicroservice/CleanArchitectureMicroservice.WebAPI/./CleanArchitectureMicroservice.WebAPI.csproj"
#COPY . .
#WORKDIR "/src/Services/CleanArchitectureMicroservice/CleanArchitectureMicroservice.WebAPI"
#RUN dotnet build "./CleanArchitectureMicroservice.WebAPI.csproj" -c $BUILD_CONFIGURATION -o /app/build
#
#FROM build AS publish
#ARG BUILD_CONFIGURATION=Release
#RUN dotnet publish "./CleanArchitectureMicroservice.WebAPI.csproj" -c $BUILD_CONFIGURATION -o /app/publish /p:UseAppHost=false
#
#FROM base AS final
#WORKDIR /app
#COPY --from=publish /app/publish .
#ENTRYPOINT ["dotnet", "CleanArchitectureMicroservice.WebAPI.dll"]

FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
WORKDIR /app
EXPOSE 8080
# Use the official .NET Core SDK as the build image
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY ["CleanArchitectureMicroservice.WebAPI.csproj", "./"]
RUN dotnet restore "./CleanArchitectureMicroservice.WebAPI.csproj"
COPY . .
WORKDIR "/src/"
RUN dotnet build "CleanArchitectureMicroservice.WebAPI.csproj" -c Release -o /app/build
FROM build AS publish
RUN dotnet publish "CleanArchitectureMicroservice.WebAPI.csproj" -c Release -o /app/publish
# Build the final image using the base image and the published output
FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "CleanArchitectureMicroservice.WebAPI.dll"]