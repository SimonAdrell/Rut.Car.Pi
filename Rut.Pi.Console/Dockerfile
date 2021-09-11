#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/runtime:3.1 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build
WORKDIR /src
COPY ["rut_car_pi/rut_pi_console/rut_pi_console.csproj", "rut_car_pi/rut_pi_console/"]
RUN dotnet restore "rut_car_pi/rut_pi_console/rut_pi_console.csproj"
COPY . .
WORKDIR "/src/rut_car_pi/rut_pi_console"
RUN dotnet build "rut_pi_console.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "rut_pi_console.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "rut_pi_console.dll"]