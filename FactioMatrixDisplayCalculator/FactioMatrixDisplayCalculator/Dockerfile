#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["FactioMatrixDisplayCalculator/FactioMatrixDisplayCalculator.csproj", "FactioMatrixDisplayCalculator/"]
RUN dotnet restore "FactioMatrixDisplayCalculator/FactioMatrixDisplayCalculator.csproj"
COPY . .
WORKDIR "/src/FactioMatrixDisplayCalculator"
RUN dotnet build "FactioMatrixDisplayCalculator.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "FactioMatrixDisplayCalculator.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "FactioMatrixDisplayCalculator.dll"]