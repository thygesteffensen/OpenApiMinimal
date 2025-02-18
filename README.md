# Minimalistic reproduction of build-time generated OpenAPI document version bug

This is to show that build-time OpenAPI document generation does not follow configured options as described in https://learn.microsoft.com/en-us/aspnet/core/fundamentals/openapi/aspnetcore-openapi?view=aspnetcore-9.0&tabs=visual-studio#lint-generated-openapi-documents-with-spectral.

This example is created by using the Microsoft WebApi template:
1.  `dotnet new webapi -n WebApi -minimal`
2. Configure OpenAPI version to be $2.0$: `options.OpenApiVersion = OpenApiSpecVersion.OpenApi2_0;` in `.AddOpenApi()`.
3. Add the `Microsoft.Extensions.ApiDescription.Server` NuGet package to emit OpenAPI document on build.


## Steps to reproduce

1. Clone repository.
2. Run `dotnet build`.
3. Open `~/WebApi/obj/WebApi.json` (OpenAPI document generated at build), it is in version $3.0$. (It should be in V2, as configured)
4. Run `dotnet run`.
5. Execute `GET {{WebApi_HostAddress}}/openapi/v1.json` form `WebApi.http`, document is in version $2.0$.

## Environment

```
$ dotnet --version
9.0.200
```

Apple M2 Pro - Sequoia 15.3
