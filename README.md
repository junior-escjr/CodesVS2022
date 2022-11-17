# CodesVS2022

> Código para rotas
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
