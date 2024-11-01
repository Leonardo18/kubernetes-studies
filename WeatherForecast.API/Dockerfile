# Etapa de build
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /app

# Copia o arquivo de solução para o diretório de trabalho
COPY WeatherForecast.API.sln ./

# Copia o projeto da API e restaura as dependências
COPY WeatherForecast.API/WeatherForecast.API.csproj WeatherForecast.API/
RUN dotnet restore WeatherForecast.API/WeatherForecast.API.csproj

# Cópia de todos os arquivos do projeto
COPY WeatherForecast.API/. WeatherForecast.API/

# Compila a aplicação
RUN dotnet publish WeatherForecast.API -c Release -o out

# Verifique se a DLL foi criada com sucesso
RUN ls -R out  # Comando para depuração, lista arquivos publicados

# Etapa de execução
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS runtime
WORKDIR /app
COPY --from=build /app/out ./

# Define a porta que a aplicação irá escutar
EXPOSE 80

# Comando para iniciar a aplicação
ENTRYPOINT ["dotnet", "WeatherForecast.API.dll"]