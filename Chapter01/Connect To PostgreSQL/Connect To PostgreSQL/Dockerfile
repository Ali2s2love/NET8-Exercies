#See https://aka.ms/customizecontainer to learn how to customize your debug container and how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
USER app
WORKDIR /app
EXPOSE 8080
#EXPOSE 8081

FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY ["Connect To PostgreSQL/Connect To PostgreSQL.csproj", "Connect To PostgreSQL/"]
RUN dotnet restore "Connect To PostgreSQL/Connect To PostgreSQL.csproj"
COPY . .
WORKDIR "/src/Connect To PostgreSQL"
RUN dotnet build "Connect To PostgreSQL.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Connect To PostgreSQL.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Connect To PostgreSQL.dll"]