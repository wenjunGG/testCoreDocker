FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 8081

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["TestNetCore/TestNetCore.csproj", "TestNetCore/"]
RUN dotnet restore "TestNetCore/TestNetCore.csproj"
COPY . .
WORKDIR "/src/TestNetCore"
RUN dotnet build "TestNetCore.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "TestNetCore.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "TestNetCore.dll"]