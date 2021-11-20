#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["Auth20ProvidersWebApp/Auth20ProvidersWebApp.csproj", "Auth20ProvidersWebApp/"]
RUN dotnet restore "Auth20ProvidersWebApp/Auth20ProvidersWebApp.csproj"
COPY . .
WORKDIR "/src/Auth20ProvidersWebApp"
RUN dotnet build "Auth20ProvidersWebApp.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Auth20ProvidersWebApp.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Auth20ProvidersWebApp.dll"]