Iniciar um projeto Web API:

```
dotnet new Web API
```

pacotes:
```
dotnet add package Microsoft.AspNetCore.Authentication.OpenIdConnect --version 5.0.1
dotnet add package Microsoft.AspNetCore.Authentication.JwtBearer --version 5.0.1
```

adiciona certificado para o web host:
```
dotnet dev-certs https --trust
```

Digite em um browswer para acessar API:
```
https://localhost:5001/swagger/
```

Entities = classes.</br>
Dtos = Data Transfer Objects (objetos que irão "levar e trazer" os dados da API (request/response)).

Adicionando dependência do MongoDB:
```
dotnet add package MongoDB.Driver
```

Para que o runtime do .NET não remova o sufixo "Async" dos métodos de ItemsController.cs, é necessário realizar a seguinte alteração em Startup.cs
```c#
public void ConfigureServices(IServiceCollection services)
{
    services.AddControllers(options => {
        options.SuppressAsyncSuffixInActionNames = false;
    });
}
```

Implementa um container para MongoDB:
```
docker run -d --rm --name mongo -p 27017:27017 -v mongodbdata:/data/db mongo
```

Digite `docker ps` para conferir se o container está de pé.

A saída será parecida com essa:
```
CONTAINER ID   IMAGE     COMMAND                  CREATED          STATUS          PORTS                                           NAMES
de429790cdf7   mongo     "docker-entrypoint.s…"   37 minutes ago   Up 37 minutes   0.0.0.0:27017->27017/tcp, :::27017->27017/tcp   mongo
```  

## Importar as especificações da API para o Postman
-----

Usaremos o [Postman](https://www.postman.com/downloads/) para trabalharmos com nossa API.

Para importar uma coleção da nossa API para o Postman (Para facilitar nossas consultas), rode o aplicativo e no browser navegue até ```https://localhost:5001/swagger/index.html```. </br>

Na parte de cima da página, logo abaixo do nome do serviço, acesse o link que será pacecido com esse: ```https://localhost:5001/swagger/v1/swagger.json```.

Será exibido um arquivo ```.json```, copie o conteúdo da página, que terá todo o *schema* da nossa API. 

Volte ao Postman acesse *import* > *raw text* e cole todo o conteúdo copiado.

No menu lateral esquerdo, clique em *Collections* e você terá a rota para os verbos HTTP de nossa API.

Ainda em *Collections*, clique nos três pontos ao lado do nome da API, clique em *Edit*, acesse *Variables* e nos campos *INITIAL VALUE* e *CURRENT VALUE* escreva a URL da nossa API, no nosso caso é ```https://localhost:5001```.


Para que possamos usar o pacote que criamos é necessário indicar onde esse pacote está. O comando deve ser executado na pasta root do projeto (que no meu caso é: ```/home/mauricio/vscodeProjects/FreeCodeCamp/Play.Catalog ```). Digite o seguinte comando no caminho acima:
```bash
dotnet nuget add source /home/mauricio/vscodeProjects/FreeCodeCamp/packages -n PlayEconomy
``` 

Para indicar a referência do pacote, navegue até a pasta onde está o arquivo .csproj e adicione a referência:
```bash
dotnet add package Play.Common
```