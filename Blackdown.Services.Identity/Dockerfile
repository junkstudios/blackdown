FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY ["Blackdown.Services.Identity/Blackdown.Services.Identity.csproj", "Blackdown.Services.Identity/"]
RUN dotnet restore "Blackdown.Services.Identity/Blackdown.Services.Identity.csproj"
COPY . .
WORKDIR "/src/Blackdown.Services.Identity"
RUN dotnet build "Blackdown.Services.Identity.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "Blackdown.Services.Identity.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Blackdown.Services.Identity.dll"]