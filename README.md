# Codes Visual Studio 2022 - .Net Core 6

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
> Exemplos de links para o menu utlizando área e sem área

```
<a class="nav-link active" aria-current="page" asp-area="" asp-controller="Home" asp-action="Index">Home</a>
<a class="nav-link" asp-area="Produtos" asp-controller="Cadastro" asp-action="Index">Cadastro</a>
```

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
