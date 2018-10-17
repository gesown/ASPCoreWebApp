FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["ASPCoreWebApp/ASPCoreWebApp.csproj", "ASPCoreWebApp/"]
RUN dotnet restore "ASPCoreWebApp/ASPCoreWebApp.csproj"
COPY . .
WORKDIR "/src/ASPCoreWebApp"
RUN dotnet build "ASPCoreWebApp.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "ASPCoreWebApp.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "ASPCoreWebApp.dll"]