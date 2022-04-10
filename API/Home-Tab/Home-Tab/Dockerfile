FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["Home-Tab/Home-Tab.csproj", "Home-Tab/"]
RUN dotnet restore "Home-Tab/Home-Tab.csproj"
COPY . .
WORKDIR "/src/Home-Tab"
RUN dotnet build "Home-Tab.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Home-Tab.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Home-Tab.dll"]
