FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
EXPOSE 80
EXPOSE 443
WORKDIR /app
COPY . .
RUN dotnet restore BlazorDevIta.Client.csproj
COPY . .
RUN dotnet build BlazorDevIta.Client.csproj -c Release -o /app/build

FROM build AS publish
RUN dotnet publish BlazorDevIta.Client.csproj -c Release -o /app/publish

FROM nginx:alpine AS final
WORKDIR /usr/share/nginx/html
COPY --from=publish /app/publish/wwwroot .
COPY --from=publish /app/publish/nginx.conf /etc/nginx/nginx.conf