FROM mcr.microsoft.com/dotnet/core/aspnet:3.0-buster-slim AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:3.0-buster AS build
WORKDIR /src
COPY ["AspNetCore30WebApi/AspNetCore30WebApi.csproj", "AspNetCore30WebApi/"]
RUN dotnet restore "AspNetCore30WebApi/AspNetCore30WebApi.csproj"
COPY . .
WORKDIR "/src/AspNetCore30WebApi"
RUN dotnet build "AspNetCore30WebApi.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "AspNetCore30WebApi.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "AspNetCore30WebApi.dll"]