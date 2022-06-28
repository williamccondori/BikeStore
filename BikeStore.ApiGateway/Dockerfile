FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["BikeStore.ApiGateway/BikeStore.ApiGateway.csproj", "BikeStore.ApiGateway/"]
RUN dotnet restore "BikeStore.ApiGateway/BikeStore.ApiGateway.csproj"
COPY . .
WORKDIR "/src/BikeStore.ApiGateway"
RUN dotnet build "BikeStore.ApiGateway.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "BikeStore.ApiGateway.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "BikeStore.ApiGateway.dll"]
