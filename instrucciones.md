# Paso a paso para la correcta implementacion de la API

Guia paso a paso para poder implementar y conectar la base de datos en sql server a la api generica para la elaboracion de la entrega #1

## Requisitos

 - <a href='https://aka.ms/ssms/22/release/vs_SSMS.exe'>SQL Server Management studio</a>
 - <a href='https://go.microsoft.com/fwlink/?linkid=2344626&clcid=0x409&culture=en-us&country=us'>SQL server 2025 Developer</a>

## Paso a paso

1. Abrir sql server management studio y ejecutar la query 

   ```SQL
      CREATE DATABASE Conocimiento_Universitario;
   ```

2. Ejecutar el codigo sql en el archivo compartido por el profesor para la creacion de tablas
 
   ```SQL
      USE Conocimiento_Universitario;
   ```
   <a href='https://correoitmedu.sharepoint.com/:t:/r/sites/580202009-8APLICACINYSERVICIOSWEBREMOTO/Materiales%20de%20clase/SCRIPT_BDCONOCIMIENTO_SIN_ESQUEMA_SQLSERVER.txt?csf=1&web=1&e=OebMHy'>SCRIPT_BDCONOCIMIENTO_SIN_ESQUEMA_SQLSERVER.txt</a>

3. Obtener las credenciales correspondientes requeridas en appsettings.json

   1. Click derecho en la instancia de sql server en el panel izquierdo de sql server management studio
   2. Click en el boton conectar
   3. ingrese a la pestaña "cadena de conexion"
   4. Copie el valor de "Data Source" y peguelo en appsettings.json de la siguiente manera

   ```json
      {
        "Jwt": {
         // ...
        },
        "TablasProhibidas": [],
        "ConnectionStrings": {
          "SqlServer": "Server=(Data Source);Database=Conocimiento_Universitario;Integrated    Security=True; TrustServerCertificate=True;",
         // ...  
        },
        "DatabaseProvider": "SqlServer"
      }
   ```

   El json completo quedaria asi:
   ```json
      {
        "Jwt": {
          "Key": "MySuperSecretKey1234567890!@#$%^&*()_+",
          "Issuer": "MyApp",
          "Audience": "MyAppUsers",
          "DuracionMinutos": 60
        },
        "TablasProhibidas": [],
        "ConnectionStrings": {
          "SqlServer": "Server=(Data Source);Database=Conocimiento_Universitario;Integrated Security=True;    TrustServerCertificate=True;",
          "LocalDb": "Server=(localdb)\\MSSQLLocalDB;Database=mi_bd;Integrated Security=True;TrustServerCertificate=True;     ",
          "Postgres": "Host=localhost;Port=5432;Database=bdfacturas_postgres_local;Username=postgres;Password=postgres;    Pooling=true;Maximum Pool Size=100;",
          "MariaDB": "Server=localhost;Port=3306;Database=mi_bd;User=root;Password=;",
          "MySQL": "Server=localhost;Port=3306;Database=mi_bd;User=root;Password=mysql;CharSet=utf8mb4;"
        },
        "DatabaseProvider": "SqlServer"
      }
   ```
   
   Importante:
      Posible error: al pegar el data sourcees posible que saque un error posiblemente sea porque el data source tiene una sola barra inclinada "\\" para arreglar el problema simplemente agregar una barra inclinada mas asi: "\\\\"
   
4. ejecutar los siguientes comandos en este orden

   ```bash

      #restaura todos los archivos necesarios
      dotnet restore

      # compila la API 
      dotnet build

      # ejecuta la API 
      dotnet run
   ```

   La pagina de documentacion de los endpoints por defecto estara alojada en:

   ```
   http://localhost:5034/swagger/index.html
   ```

