# Dockerfile
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY ["KubernetesApiApp/KubernetesApiApp.csproj", "KubernetesApiApp/"]
RUN dotnet restore "KubernetesApiApp/KubernetesApiApp.csproj"
COPY . .
WORKDIR "/src/KubernetesApiApp"
RUN dotnet build "KubernetesApiApp.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "KubernetesApiApp.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "KubernetesApiApp.dll"]
