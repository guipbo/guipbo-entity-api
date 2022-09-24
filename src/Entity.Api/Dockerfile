#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["Entity.Api/Entity.Api.csproj", "Entity.Api/"]
RUN dotnet restore "Entity.Api/Entity.Api.csproj"
COPY . .
WORKDIR "/src/Entity.Api"
RUN dotnet build "Entity.Api.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Entity.Api.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Entity.Api.dll"]