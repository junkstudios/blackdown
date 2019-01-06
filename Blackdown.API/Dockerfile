FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY ["Blackdown.API/Blackdown.API.csproj", "Blackdown.API/"]
RUN dotnet restore "Blackdown.API/Blackdown.API.csproj"
COPY . .
WORKDIR "/src/Blackdown.API"
RUN dotnet build "Blackdown.API.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "Blackdown.API.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Blackdown.API.dll"]