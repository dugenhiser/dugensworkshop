FROM microsoft/dotnet:2.1-aspnetcore-runtime-nanoserver-1709 AS base
WORKDIR /app
EXPOSE 65402
EXPOSE 44350

FROM microsoft/dotnet:2.1-sdk-nanoserver-1709 AS build
WORKDIR /src
COPY dugensworkshop2/dugensworkshop2.csproj dugensworkshop2/
RUN dotnet restore dugensworkshop2/dugensworkshop2.csproj
COPY . .
WORKDIR /src/dugensworkshop2
RUN dotnet build dugensworkshop2.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish dugensworkshop2.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "dugensworkshop2.dll"]
