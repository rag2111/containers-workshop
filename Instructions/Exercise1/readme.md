# Create a "Hello World" application in .NET 8 and Dockerize it

## Prerequisites
1. **.Net Framework v.8.0**:  Ensure you have the .NET SDK 8 installed. You can download it [here](https://dotnet.microsoft.com/download).
3. **Docker**: Make sure Docker is installed and running on your machine. Download it [here](https://www.docker.com/products/docker-desktop).

## Steps

1. **Create a new .NET 8 application:**
    ```bash
    dotnet new webapi -n HelloWorld
    cd HelloWorld
    ```

2. **Modify the `Program.cs` file:**
    ```csharp
    var builder = WebApplication.CreateBuilder(args);
    var app = builder.Build();

    app.MapGet("/", () => "Hello World");

    app.Run();
    ```

3. **Test the application locally:**
    ```bash
    dotnet run
    ```

4. **Create a `Dockerfile`:**
    ```dockerfile
    FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
    WORKDIR /app

    COPY *.csproj .
    RUN dotnet restore

    COPY . .
    RUN dotnet publish -c Release -o out

    FROM mcr.microsoft.com/dotnet/aspnet:8.0
    WORKDIR /app
    COPY --from=build /app/out .

    EXPOSE 80
    ENTRYPOINT ["dotnet", "HelloWorld.dll"]
    ```

5. **Build the Docker image:**
    ```bash
    docker build -t helloworld-dotnet:1-0 .
    ```

6. **Run the Docker container:**
    ```bash
    docker run -d -p 8080:80 helloworld-dotnet:1-0
    ```

Done! Now you have a "Hello World" application in .NET 8 running in a Docker container.