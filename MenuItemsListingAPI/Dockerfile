FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443
FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["MenuItemsListingAPI/MenuItemsListingAPI.csproj", "MenuItemsListingAPI/"]
RUN dotnet restore "MenuItemsListingAPI/MenuItemsListingAPI.csproj"
COPY . .
WORKDIR "/src/MenuItemsListingAPI"
RUN dotnet build "MenuItemsListingAPI.csproj" -c Release -o /app/build
FROM build AS publish
RUN dotnet publish "MenuItemsListingAPI.csproj" -c Release -o /app/publish
FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "MenuItemsListingAPI.dll"]