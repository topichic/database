## Dockerfile. Приложение на C#
### 1. Структура проекта
```
MyApp/
├── Dockerfile
├── MyApp.csproj
├── Program.cs
```

В каталоге для Docker-проектов создать одной bash-командой всю структуру для нового приложения:
```shell
mkdir -p MyApp && touch MyApp/Program.cs MyApp/MyApp.csproj MyApp/Dockerfile && cd MyApp
```

### 2. Содержимое файла `MyApp.csproj`
```xml
<Project Sdk="Microsoft.NET.Sdk.Web">
  <PropertyGroup>
    <TargetFramework>net8.0</TargetFramework>
    <Nullable>enable</Nullable>
    <ImplicitUsings>enable</ImplicitUsings>
  </PropertyGroup>
</Project>
```

### 3. Содержимое файла `Program.cs`
```c#
var app = WebApplication.Create(args);
// Определяем маршрут для корневого URL
app.MapGet("/", () => "Hello from Docker! Привет из Docker!");
// Запускаем приложение, слушая порт 80 на всех интерфейсах
app.Run("http://*:80");
```


### 4. Содержимое файла `Dockerfile`:
```dockerfile
# Используем SDK для сборки
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
# Копируем файлы проекта и восстанавливаем зависимости
COPY ["MyApp.csproj", "."]
RUN dotnet restore "MyApp.csproj"
# Копируем весь код и публикуем приложение
COPY . .
RUN dotnet publish "MyApp.csproj" -c Release -o /app/publish
# Финальный образ с рантаймом
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS runtime
WORKDIR /app
COPY --from=build /app/publish .
# Открываем порт
EXPOSE 80
# Запускаем приложение
ENTRYPOINT ["dotnet", "MyApp.dll"]
```

### 5. Сборка проекта

В командной строке, находясь в папке `MyApp`, выполнить:
```shell
docker build -t myapp .
```
> Флаг `-t` задает имя образа

### 6. Запуск проекта
```shell
docker run -d -p 8081:80 --name myapp myapp
```

После запуска откройте браузер по адресу [http://localhost:8081](http://localhost:8081) — вы должны увидеть сообщение **Hello from Docker! Привет из Docker!**

![](/MyNotes\img\TASKDockerfile.png)