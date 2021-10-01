#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["src/OpenSpace.Host/OpenSpace.Host.csproj", "src/OpenSpace.Host/"]
RUN dotnet restore "src/OpenSpace.Host/OpenSpace.Host.csproj"
COPY . .
WORKDIR "/src/src/OpenSpace.Host"
RUN dotnet build "OpenSpace.Host.csproj" -c Release -o /app/build --no-restore

FROM build AS publish
RUN dotnet publish "OpenSpace.Host.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "OpenSpace.Host.dll"]