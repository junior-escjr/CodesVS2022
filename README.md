# Codes Visual Studio 2022 - .Net Core 6

## Rotas
> Código para rotas. Adicionar esse código no arquivo `Program.cs`.
```
app.UseEndpoints(endpoints =>
{

    endpoints.MapControllerRoute(
      name: "areas",
      pattern: "{area:exists}/{controller=Home}/{action=Index}/{id?}"
    );

    endpoints.MapControllerRoute(
        name: "default",
        pattern: "{controller=Home}/{action=Index}/{id?}"
    );
});
```
> código especifico para uso de rotas com `Areas`

```
endpoints.MapAreaControllerRoute(
        name: "AreaVendas",
        areaName: "Vendas",
        pattern: "Vendas/{controller=Pedidos}/{action=Index}/{id?}"
    );
```

## Links
> Exemplos de links para o menu utlizando área e sem área

```
<a class="nav-link active" aria-current="page" asp-area="" asp-controller="Home" asp-action="Index">Home</a>
<a class="nav-link" asp-area="Produtos" asp-controller="Cadastro" asp-action="Index">Cadastro</a>
```

## Arquivos
> BundleConfig - exemplo de código para utilizar o bundleconfig para automatizar a minificação dos arquivos .css e .js. Para funcionar no `VS 2022` tem que instalar uma extensão chamada `Bundler e Minifier 2022+`. Sem essa extensão a `Task Runner Explorer` não reconhece o arquivo bundleconfig.json.
```
[
  {
    "outputFileName": "wwwroot/static/css/all.min.css",
    "inputFiles": [
      "wwwroot/lib/font-awesome/css/fontawesome.css",
      "wwwroot/lib/bootstrap/css/bootstrap.css",
      "wwwroot/src/css/site.css"
    ]
  },
  {
    "outputFileName": "wwwroot/static/js/all.min.js",
    "inputFiles": [
      "wwwroot/lib/jquery/jquery.js",
      "wwwroot/src/js/site.js"
    ]
  }
]
```

> Código para funcionar arquivos estáticos `(.css, .js)`.

```
app.UseStaticFiles();
```

## Connection Strings
> Para funcionar o código abaixo tem que instalar através do `Manage NuGet` o pacote do `Microsoft.EntityFrameworkCore.SqlServer` compatível com a versão atual do software utilizado
```
UseSqlServer
```

> Código da `ConnectionStrings`
```
"AllowedHosts": "*",
  "ConnectionStrings": {
    "MeuDbContext": "Server=(localdb)\\MSSQLLocalDB;Database=NomeDoBancoDeDados;Trusted_Connection=True;MultipleActiveResultSets=true"
  }
```

> Duas formas de conectar com a database. Adicionar ambos os códigos no arquivo `Program.cs`.
```
string connString = builder.Configuration.GetConnectionString("MeuDbContext");
```
ou
```
builder.Services.AddDbContext<MeuDbContext> (options => {
    options.UseSqlServer(builder.Configuration.GetConnectionString("MeuDbContext"));
});
```

> Instância de conexão local

```
Server=(localdb)\\MSSQLLocalDB;
```


## Migrations
> Para funcionar o código abaixo tem que instalar através do `Manage NuGet` o pacote do `Microsoft.EntityFrameworkCore.Tools` compatível com a versão atual do software utilizado
```
add-migration "Inicial" -Verbose
```

## Outros
> Altera a nomenclatura da pasta `Área` para `Modulos`. Adicionar esse código no arquivo `Program.cs` abaixo da variável `builder`. Não esquecer de alterar o namespace do controller para o nome novo.

```
builder.Services.Configure<RazorViewEngineOptions>(options =>
{
    options.AreaViewLocationFormats.Clear();
    options.AreaViewLocationFormats.Add("/Modulos/{2}/Views/{1}/{0}.cshtml");
    options.AreaViewLocationFormats.Add("/Modulos/{2}/Views/Shared/{0}.cshtml");
    options.AreaViewLocationFormats.Add("/Views/Shared/{0}.cshtml");
});
```
