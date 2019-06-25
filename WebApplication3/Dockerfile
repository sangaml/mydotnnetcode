FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["WebApplication3/WebApplication3.csproj", "src/"]
RUN dotnet restore "src/WebApplication3.csproj"
COPY . .
WORKDIR "/src"
RUN dotnet build "src/WebApplication3.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "src/WebApplication3.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "WebApplication3.dll"]
