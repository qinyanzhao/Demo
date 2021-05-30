#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["src/Sky.Ms.WebApi/Sky.Ms.WebApi.csproj", "src/Sky.Ms.WebApi/"]
RUN dotnet restore "src/Sky.Ms.WebApi/Sky.Ms.WebApi.csproj"
COPY . .
WORKDIR "/src/src/Sky.Ms.WebApi"
RUN dotnet build "Sky.Ms.WebApi.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Sky.Ms.WebApi.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Sky.Ms.WebApi.dll"]