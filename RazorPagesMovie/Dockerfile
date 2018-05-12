FROM microsoft/aspnetcore:2.0-nanoserver-1709 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0-nanoserver-1709 AS build
WORKDIR /src
COPY RazorPagesMovie/RazorPagesMovie.csproj RazorPagesMovie/
RUN dotnet restore RazorPagesMovie/RazorPagesMovie.csproj
COPY . .
WORKDIR /src/RazorPagesMovie
RUN dotnet build RazorPagesMovie.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish RazorPagesMovie.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "RazorPagesMovie.dll"]
