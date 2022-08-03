# Consulta Saldos e Limites de Anúncios

A medida que os anúncios são publicados, o limite disponível em seu plano contratado é consumido. A API abaixo disponibiliza informações para acompanhamento do limite de inserção de um plano, a quantidade de inserções que já foram realizadas, o saldo disponível para inserções de novos anúncios, a data da última renovação do plano e a data que a próxima renovação do plano ocorrerá.

---
## Requisição de consulta de saldo e limite

A URL usada para fazer a requisição do arquivo JSON é https://apps.olx.com.br/autoupload/balance, método `GET`. Essa requisição deve conter o `access_token` de cada anunciante no header como: `Authorization: Bearer <access_token>`.

> O campo `access_token` pode ser obtido seguindo a documentação [Autenticação na API olx.com.br](oauth.md).


## Retorno de sucesso esperado 

Se o anunciante possui um plano profissional ativo, a consulta retorna um `status code 200` e um JSON no corpo da resposta com a estrutura: 

| Parâmetro | Valores | Obrigatório | Descrição  |
|-----------|---------|-------------|------------|
| `id` | `string` | sim | Identificador único do plano profissinal | 
| `name` | `string` | sim | Descrição do plano profissional | 
| `ads` | [**balance**](#balance) | sim | Estrutura contendo quantidade de inserções do cliente, saldo do cliente e limite de inserções do plano |
| `last_renew_date` | `string (ISO Datetime)` | sim | Data da última renovação de saldo de anúncios. <br><br>*Observe que esta data e hora estão no Zulu Time Zone. Para horário de Brasília, decremente três horas.* |
| `next_renew_date` | `string (ISO Datetime)` | sim | Data da próxima renovação de saldo de anúncios. <br><br>*Observe que esta data e hora estão no Zulu Time Zone. Para horário de Brasília, decremente três horas.* |
</br>

### *balance*

| Parâmetro | Valores | Obrigatório | Descrição  |
|-----------|---------|-------------|------------|
| `performed` | `integer` | sim | Inserções já realizadas |
| `available` | `integer` | sim | Saldo disponível para uso |
| `total` | `integer` | sim | Limite contratado pelo cliente |


## Retorno de erro esperado

Caso ocorra algum erro ou o anunciante não possua plano profissional ativo, a consulta retorna um `status code > 200` e um JSON com o motivo e a mensagem do erro.
</br>

## Códigos e motivos de erros da requisição retornados

| <p align="center">Status Code</p> | Descrição | Motivo | Mensagem |
|--------|-----------|----------------|----------|
| <p align="center">`400`</p> | Falta campo de `authorization` no header da requisição | BAD_REQUEST | Check the header field(s) |
| <p align="center">`401`</p> | Token inválido | ACCESS_DENIED | Check the client authentication token |
| <p align="center">`410`</p> | Cliente não possui planos com limites | PRODUCT_NOT_FOUND_BY_ACCOUNT | Plan does not control limits |
| <p align="center">`429`</p> | Rate Limit configurado quando o cliente fazer mais requisições por segundo do que deveria | RATE_LIMIT | You have exceeded the X requests in X seconds limit! |
| <p align="center">`500`</p> | Erro interno inesperado | UNEXPECTED_INTERNAL_ERROR | Unexpected internal error. Try again later |
</br>

## Exemplos de retorno
</br>

> Para um plano com limite de 20 inserções de anúncios no qual nenhum anúncio foi inserido:

* Request 

    ```sh
    curl -A Mozila -H "Authorization: Bearer <access_token>" "https://apps.olx.com.br/autoupload/balance"
    ```

* Response

    ```json
    HTTP/1.1 200 OK
    Content-Type: application/json;charset=UTF-8
    Cache-Control: no-store
    Pragma: no-cache

    {
        "id": "cc07f89f5f9b691a4bc24d98614e54df",
        "name": "Plano Profissional - Carros 20",
        "ads": {
            "performed": 0,
            "available": 20,
            "total": 20
        },
        "last_renew_date": "2022-06-30T16:36:32.069324",
        "next_renew_date": "2022-07-29T16:36:32.069324"
    }
    ```
---
> Para um plano com limite de 20 inserções de anúncios no qual 5 anúncios foram inseridos:

* Request
    ```sh
    curl -A Mozila -H "Authorization: Bearer <access_token>" "https://apps.olx.com.br/autoupload/balance"
    ```

* Response

    ```json
    HTTP/1.1 200 OK
    Content-Type: application/json;charset=UTF-8
    Cache-Control: no-store
    Pragma: no-cache

    {
        "id": "cc07f89f5f9b691a4bc24d98614e54df",
        "name": "Plano Profissional - Carros 20",
        "ads": {
            "performed": 5,
            "available": 15,
            "total": 20
        },
        "last_renew_date": "2022-06-30T16:36:32.069324",
        "next_renew_date": "2022-07-29T16:36:32.069324"
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
> Para um anunciante que não possui plano profissional ativo:

* Request
    ```sh
    curl -A Mozila -H "Authorization: Bearer <access_token>" "https://apps.olx.com.br/autoupload/balance"
    ```

* Reponse

    ```json
    HTTP/1.1 410
    Content-Type: application/json;charset=UTF-8
    Cache-Control: no-store
    Pragma: no-cache

    {
        "reason": "PRODUCT_NOT_FOUND_BY_ACCOUNT", 
        "message": "Plan does not control limits."
    }
    ```
