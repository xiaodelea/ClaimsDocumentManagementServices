FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY ["ClaimsDocumentManagementServices/ClaimsDocumentManagementServices.csproj", "ClaimsDocumentManagementServices/"]
RUN dotnet restore "ClaimsDocumentManagementServices/ClaimsDocumentManagementServices.csproj"
COPY . .
WORKDIR "/src/ClaimsDocumentManagementServices"
RUN dotnet build "ClaimsDocumentManagementServices.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "ClaimsDocumentManagementServices.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "ClaimsDocumentManagementServices.dll"]