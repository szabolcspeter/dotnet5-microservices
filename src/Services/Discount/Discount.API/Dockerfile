FROM mcr.microsoft.com/dotnet/aspnet:5.0-focal AS base
WORKDIR /app
EXPOSE 80

ENV ASPNETCORE_URLS=http://+:80

FROM mcr.microsoft.com/dotnet/sdk:5.0-focal AS build
WORKDIR /src
COPY ["src/Services/Discount/Discount.API/Discount.API.csproj", "src/Services/Discount/Discount.API/"]
RUN dotnet restore "src/Services/Discount/Discount.API/Discount.API.csproj"
COPY . .
WORKDIR "/src/src/Services/Discount/Discount.API"
RUN dotnet build "Discount.API.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Discount.API.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Discount.API.dll"]
