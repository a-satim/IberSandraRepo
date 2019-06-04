	FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["IbercajaPoC/IbercajaPoC.csproj", "IbercajaPoC/"]
RUN dotnet restore "IbercajaPoC/IbercajaPoC.csproj"
COPY . .
WORKDIR "/src/IbercajaPoC"
RUN dotnet build "IbercajaPoC.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "IbercajaPoC.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "IbercajaPoC.dll"]