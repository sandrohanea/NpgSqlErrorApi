#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0-alpine AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0-alpine AS build
WORKDIR /src
COPY ["NpgSqlErrorApi/NpgSqlErrorApi.csproj", "NpgSqlErrorApi/"]
RUN dotnet restore "NpgSqlErrorApi/NpgSqlErrorApi.csproj"
COPY . .
WORKDIR "/src/NpgSqlErrorApi"
RUN dotnet build "NpgSqlErrorApi.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "NpgSqlErrorApi.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "NpgSqlErrorApi.dll"]