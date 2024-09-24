FROM mcr.microsoft.com/dotnet/runtime:6.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["ISI_1/ISI_1.csproj", "ISI_1/"]
RUN dotnet restore "ISI_1/ISI_1.csproj"
COPY . .
WORKDIR "/src/ISI_1"
RUN dotnet build "ISI_1.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "ISI_1.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "ISI_1.dll"]
