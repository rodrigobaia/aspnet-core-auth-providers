#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["Auth20ProvidersWebApi/Auth20ProvidersWebApi.csproj", "Auth20ProvidersWebApi/"]
RUN dotnet restore "Auth20ProvidersWebApi/Auth20ProvidersWebApi.csproj"
COPY . .
WORKDIR "/src/Auth20ProvidersWebApi"
RUN dotnet build "Auth20ProvidersWebApi.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Auth20ProvidersWebApi.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Auth20ProvidersWebApi.dll"]