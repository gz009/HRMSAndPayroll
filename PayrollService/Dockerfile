FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY ["PayrollService/PayrollService.csproj", "PayrollService/"]
RUN dotnet restore "PayrollService/PayrollService.csproj"
COPY . .
WORKDIR "/src/PayrollService"
RUN dotnet build "PayrollService.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "PayrollService.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "PayrollService.dll"]
