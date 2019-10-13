FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["DevUp2019Test.Web/DevUp2019Test.Web.csproj", "DevUp2019Test.Web/"]
RUN dotnet restore "DevUp2019Test.Web/DevUp2019Test.Web.csproj"
COPY . .
WORKDIR "/src/DevUp2019Test.Web"
RUN dotnet build "DevUp2019Test.Web.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "DevUp2019Test.Web.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "DevUp2019Test.Web.dll"]