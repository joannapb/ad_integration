# Aplicando destaques aos anúncios

Com o passar do tempo, um anúncio publicado no portal descerá algumas posições, seguindo-se uma ordenação natural de inserções. Para que o anúncio volte ao topo novamente, oferecemos os **destaques** que são benefícios para que o anúncio ganhe mais visibilidade na OLX. Dentre eles, oferecemos os **Destaques Pro** exclusivamente para que os clientes profissionais possam evidenciar seus anúncio de forma com que eles voltarão aos primeiros resultados como se fosse um anúncio novo.

---
## Consulta dos anúncio em destaque

Em breve. 

---
## Aplicação de destaque em anúncio

A URL usada para fazer a requisição do arquivo JSON é https://apps.olx.com.br/autoupload/bump/ad/{ad_id}, método `PUT`. Essa requisição deve conter o `token` de cada anunciante no header como: `Authorization: Bearer <token>`.

> O campo `access_token` pode ser obtido seguindo a documentação [Autenticação na API olx.com.br](oauth.md).

| Parâmetro | Valores | Obrigatório | Descrição  |
|-----------|---------|-------------|------------|
| `ad_id` | `string` | sim | Para importação via JSON, o identificador é o parâmetro id existente em cada anúncio. | 
| `token` | `string` | sim | N/A | 

</br>

Se o anunciante possui um plano profissional ativo e o destaque for aplicado, a requisição retorna um `status code 200` e um JSON no corpo da resposta com a estrutura: 
## Retorno de sucesso esperado 

| Parâmetro | Valores | Obrigatório | Descrição  |
|-----------|---------|-------------|------------|
| `next_bumps` | `arrayOf[string (ISO Datetime)]` | sim | Próximas datas agendadas para a volta do anúncio ao topo (ou seja, para a reaplicação do destaque). | 

</br>

## Retorno de erro esperado

Caso ocorra algum erro ou o anunciante não possua plano profissional ativo, a consulta retorna um `status code > 400` e um JSON com o motivo e a mensagem do erro.
</br>

## Códigos e motivos de erros da requisição retornados

| <p align="center">Status Code</p> | Descrição | Motivo | Mensagem |
|--------|-----------|----------------|----------|
| <p align="center">`400`</p> | Falta campo de `authorization` no header da requisição | BAD_REQUEST | Check the header field(s) |
| <p align="center">`401`</p> | Token inválido | ACCESS_DENIED | Check the client authentication token |
| <p align="center">`403`</p> | Cliente não tem saldo disponível para aplicar o destaque | FORBIDDEN | `{ "reason": "FORBIDDEN", "message": "Forbidden." }` |
| <p align="center">`404`</p> | Anúncio não encontrado | NOT FOUND | `{ "reason": "NOT_FOUND", "message": "Ad not found." }` |
| <p align="center">`422`</p> | Bump já aplicado | BUMP_ALREADY_APPLIED_OR_NOT_SYNCHRONIZED | `{ "reason": "BUMP_ALREADY_APPLIED_OR_NOT_SYNCHRONIZED", "message": "Bump already applied or Ad not synchronized." }` |
| <p align="center">`429`</p> | Rate Limit configurado quando o cliente fazer mais requisições por segundo do que deveria | RATE_LIMIT | You have exceeded the X requests in X seconds limit! |
| <p align="center">`500`</p> | Erro interno inesperado | UNEXPECTED_INTERNAL_ERROR | Unexpected internal error. Try again later |
</br>

## Exemplos de retorno
</br>

> Ao aplicar o destaque datas agendadas para a volta do anúncio ao topo (ou seja, para a reaplicação do destaque)


* Request 

    ```sh
    curl -X PUT "https://apps.olx.com.br/autoupload/bump/ad/{ad_id}" -H "accept: application/json" -H "Content-Type: application/json" -H "authorization: Bearer {token}"
    ```

* Response

    ```json
    HTTP/1.1 200 OK
    Content-Type: application/json;charset=UTF-8
    Cache-Control: no-store
    Pragma: no-cache

    {
        "next_bumps": ["2020-09-01 00:00:00.00000", "2020-09-05 00:00:00.00000"]
    }
    ```
---
> Em caso de erro

* Request
    ```sh
    curl -X PUT "https://apps.olx.com.br/autoupload/bump/ad/{ad_id}" -H "accept: application/json" -H "Content-Type: application/json" -H "authorization: Bearer {token}"
    ```

* Response

    ```json
    HTTP/1.1 404
    Content-Type: application/json;charset=UTF-8
    Cache-Control: no-store
    Pragma: no-cache

    {
        "reason": "NOT_FOUND",
        "message": "Ad not found."
    }
    ```
---
> Para uma requisição com `access_token` inválido:

* Request
    ```sh
    curl -A Mozila -H "Authorization: Bearer <access_token>" "https://apps.olx.com.br/autoupload/balance"
    ```

* Response

    ```json
    HTTP/1.1 401 
    Content-Type: application/json;charset=UTF-8
    Cache-Control: no-store
    Pragma: no-cache

    {
        "reason": "ACCESS_DENIED", 
        "message": "Check the client authentication token."
    }
    ```
---
> Para o anúncio que já foi dado destaque:

* Request
    ```sh
    curl -X PUT "https://apps.olx.com.br/autoupload/bump/ad/{ad_id}" -H "accept: application/json" -H "Content-Type: application/json" -H "authorization: Bearer {token}"
    ```

* Reponse

    ```json
    HTTP/1.1 422
    Content-Type: application/json;charset=UTF-8
    Cache-Control: no-store
    Pragma: no-cache

    { 
        "reason": "BUMP_ALREADY_APPLIED_OR_NOT_SYNCHRONIZED", 
        "message": "Bump already applied or Ad not synchronized." 
    }
    ```
