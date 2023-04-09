<h1 align="center">
  <a name="logo" href="https://carris.pt/"><img src="https://www.carris.pt/media/q04iikx3/logosvg.svg" alt="Logótipo Carris" width="400"></a>
  <br>
  Unofficial Carris API Documentation
</h1>
<h4 align="center">API privada da Carris, descrita de acordo com as normas OpenAPI 3.0.0 e Swagger.</h4>
<h6 align="center">Esta API está protegida com autorização do tipo bearer JWT. Os tokens expiram a cada 15 minutos e devem ser atualizados com refresh.</h6>
<p align="center"><a href="https://joaodcp.github.io/Carris-API/">Documentação Swagger/OpenAPI</a></p>
<hr>
<h3 align="center">A CARRIS também disponibiliza dados publicamente nos formatos GTFS e GTFS-RT através do seu portal do programador (https://gateway.carris.pt/apiui/#!/)</h4>
<hr>

## Índice de Conteúdos
<details>
<summary>Clique para expandir</summary>

- [Autenticação Inicial](#auth)
  * [Pedido](#auth-req)
  * [Resposta](#auth-res)
- [Endpoints](#endpoints)
  * [Pedido](#endpoints-req)
  * [Resposta](#endpoints-res)
- [Refresh/Atualização](#refresh)
  * [Pedido](#refresh-req)
  * [Resposta](#refresh-res)


</details>

<hr>
<h1 id="auth">..::Autenticação Inicial::..</h1>
<h2>Obter um authorizationToken inicial</h2>
<h4>Fazer um POST request para o <a href="https://joaodcp.github.io/Carris-API/#/Authentication/GetBearerTokenJWT">endpoint de autorização</a>.</h4> 

<h3 id="auth-req">Pedido</h3>

```javascript
{
	"token": "string",    //o valor desta chave é token de app fornecido pela carris
	"type": "string"    //o valor desta chave deverá ser "apikey" no primeiro request
}
```
<h3 id="auth-res">Resposta</h3>

```javascript
{
  "authorizationToken": "string",    // guardar token JWT a usar em todas os outros pedidos
  "refreshToken": "string",    // guardar token para atualizar o token expirado
  "expires": int    // data de expiração do token em segundos desde a Era Unix/Unix Epoch
}
```

<p>Pode descodificar o token JWT "authorizationToken" e saber mais sobre a norma JWT em <a href="https://jwt.io/">JWT.io</a>

<h1 id="endpoints">..::Endpoints::..</h1>
<h2>Obter dados provenientes da Carris</h2>
<h4>Fazer GET requests para os <a href="https://joaodcp.github.io/Carris-API/">endpoints de dados</a>.</h4> 

<h3 id="endpoints-req">Pedido</h3>
<h4>Deverá incluir um cabeçalho de autenticação do tipo Bearer, que contenha o o valor da chave JSON obtido em <a href="#auth">Autenticação Inicial</a>:</h4>

```
Authorization: Bearer { authorizationToken }
```

<h3 id="endpoints-res">Resposta</h3>
<h4>Deverá recebr uma respota em troca do seu pedido.</h4>

```
A resposta depende do endpoint que escolher. 
Será dada no formato JSON.
```

<h1 id="refresh">..::Refresh/Atualização::..</h1>
<h2>Trocar o seu authenticationToken inválido por um válido</h2>
<h4>Após aproximadamente 15 minutos (se preferir, calcule a hora de criação do token com a hora de expiração do mesmo para obter o tempo de vida do token), o seu authorizationToken irá expirar. Recolha o refreshToken que obteu em <a href="#auth">Autenticação Inicial</a> e inclua-o no corpo do seu pedido. Ser-lhe-á atribuído um novo authorizationToken válido.</h4>

<h6>Repita este processo ao longo do tempo de vida da sua aplicação (faça um novo pedido de <a href="#auth">Autenticação Inicial</a> se o tempo de vida da app for reiniciado). A cada 15 minutos, revogue o authorizationToken atual e atualize-o - e assim sucessivamente.</h6>

<h3 id="refresh-req">Pedido</h3>
<h4>Agora, deverá recolher o refreshToken obtido em <a href="#auth">Autenticação Inicial</a> e faça dele o valor da chave "token". Indique que o token é de atualização, mudando o valor da chave "type" para "refresh".</h4>

```javascript
{
	"token": "string",    // token de refresh
	"type": "string"    // o valor desta chave deve ser "refresh" aquando da atualização do seu token
}
```
<h3 id="refresh-res">Resposta</h3>
<h4>Esta resposta será igual à obtida em <a href="#auth">Autenticação Inicial</a>. Recolha os valores da chave e use-os nos seus próximos pedidos, de forma a manter um flow de tokens contínuo. Aquando do término de mais um período de 15 minutos, volte a atualizar o seu authorizationToken e assim sucessivamente!</h4>

```javascript
{
  "authorizationToken": "string",    // guardar token a usar em todas os outros pedidos
  "refreshToken": "string",    // guardar token para atualizar o token expirado
  "expires": int    // data de expiração do token em segundos desde a Era Unix/Unix Epoch
}
```

<hr>
<h2>Divirta-se e partilhe os seus projetos connosco!</h2>
<h3>Não hesite em contactar para mais informações!</h3>
<h4>Os Pull Requests e Issues são bem-vindos :)</h4>
