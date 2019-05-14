FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["DemoApp/DemoApp.csproj", "DemoApp/"]
RUN dotnet restore "DemoApp/DemoApp.csproj"
COPY . .
WORKDIR "/src/DemoApp"
RUN dotnet build "DemoApp.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "DemoApp.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "DemoApp.dll"]