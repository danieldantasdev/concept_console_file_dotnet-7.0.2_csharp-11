FROM mcr.microsoft.com/dotnet/runtime:7.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["Directory/Directory.csproj", "Directory/"]
RUN dotnet restore "Directory/Directory.csproj"
COPY . .
WORKDIR "/src/Directory"
RUN dotnet build "Directory.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Directory.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Directory.dll"]
