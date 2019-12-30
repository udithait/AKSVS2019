FROM mcr.microsoft.com/dotnet/core/aspnet:3.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:3.0 AS build
WORKDIR /src
COPY ["aksdemo2/aksdemo2.csproj", "aksdemo2/"]

RUN dotnet restore "aksdemo2/aksdemo2.csproj"
COPY . .
WORKDIR "/src/aksdemo2"
RUN dotnet build "aksdemo2.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "aksdemo2.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "aksdemo2.dll"]