<h1 align="center">
  <a name="logo" href="https://carris.pt/"><img src="https://www.carris.pt/media/q04iikx3/logosvg.svg" alt="Logótipo Carris" width="400"></a>
  <br>
  Unofficial Carris API Documentation
</h1>
<h4 align="center">API privada da Carris, descrita de acordo com a norma OpenAPI 3.0.0 e Swagger.</h4>
<h6 align="center">Esta API está protegida com autorização do tipo bearer JWT. Os tokens expiram a cada 15 minutos e devem ser atualizados com refresh.</h6>
<hr>
<h1>..::Autenticação::..</h1>
<h2>Obter um authorizationToken inicial</h2>
<h4>Fazer um POST request para o <a href="https://joaodcp.github.io/Carris-API/#/Authentication/GetBearerTokenJWT">endpoint de autorização</a>.</h4> 

<h3>Pedido</h3>

```javascript
{
	"token": "string",    //token de app fornecido pela carris
	"type": "string"    //"apikey" no primeiro request
}
```
<h3>Resposta</h3>

```javascript
{
  "authorizationToken": "string",    //guardar token a usar em todas os outros pedidos
  "refreshToken": "string",    //guardar token para atualizar o token expirado
  "expires": int    // data de expiração do token em segundos desde a Era Unix/Unix Epoch
}
```
