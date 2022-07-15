# Listagem de Marcas e Modelos de Automóveis e Motos na OLX

Os endpoints disponíveis para consultar detalhes de marcas, modelos, versões e cilindradas para Automóveis e Motos na OLX são os seguintes:

| Endpoint | Subcategoria | Descrição |
|----------------------------------------------------------------------|--------------|--------------------------------------------------------|
| https://apps.olx.com.br/autoupload/car_info | Carros | Marcas de carros disponíveis |
| https://apps.olx.com.br/autoupload/car_info/{id_marca} | Carros | Modelos de carros de uma determinada marca |
| https://apps.olx.com.br/autoupload/car_info/{id_marca}/{id_modelo} | Carros | Versões de um modelo de carro de uma determinada marca |
| https://apps.olx.com.br/autoupload/moto_info | Motos | Marcas de motos disponíveis |
| https://apps.olx.com.br/autoupload/moto_info/{id_marca} | Motos | Modelos de motos de uma determinada marca |
| https://apps.olx.com.br/autoupload/moto_info/{id_marca}/{id_modelo} | Motos | Versões de um modelo de moto de uma determinada marca |
| https://apps.olx.com.br/autoupload/moto_cubiccms_info | Motos | Cilindradas disponíveis para motos |

Nosso servidor deve receber a requisição com método do tipo `POST`, sendo que o formato do arquivo a ser enviado para nosso servidor deverá ser do tipo JSON.

## Automóveis

### Marcas de Carros Disponíveis

Exemplo de chamada: `POST` https://apps.olx.com.br/autoupload/car_info:

Utilizando o cURL:

```bash
$ curl -A Mozila -L -X POST 'https://apps.olx.com.br/autoupload/car_info' -H 'Content-Type: application/json' --data-raw '{
    "access_token": "ca18abccaadd282490e75173f98b8ec6f0c1c6c8"
}'
```

Utilizando postman/insomnia:

```json
{
    "access_token":"ca18abccaadd282490e75173f98b8ec6f0c1c6c8"
}
```

Exemplo de retorno:

```json
{
    "status": "ok",
    "data": {
        "AM GEN": 1,
        "ACURA": 2,
        "AGRALE": 3,
        "ALFA ROMEO": 4,
        "ASIA MOTORS": 5,
        "AUDI": 6,
        "BMW": 7,
        "BRM": 8,
        "BUGGY": 9,
        "BUGRE": 10,
        "CBT JIPE": 11,
        "CHANGAN": 12
    }
}
```


### Modelos de Carros de Determinada Marca

Exemplo de chamada: `POST` https://apps.olx.com.br/autoupload/car_info/6 (no caso, o id `6` é a marca `AUDI`, conforme visto no exemplo acima):

Utilizando o cURL:

```bash
$ curl -A Mozila -L -X POST 'https://apps.olx.com.br/autoupload/car_info/6' -H 'Content-Type: application/json' --data-raw '{
    "access_token": "ca18abccaadd282490e75173f98b8ec6f0c1c6c8"
}'
```

Utilizando postman/insomnia:

```json
{
    "access_token": "ca18abccaadd282490e75173f98b8ec6f0c1c6c8"
}
```

Exemplo de retorno: 

```json
{
    "status": "ok",
    "data": {
        "80": 2,
        "100": 1,
        "A1": 3,
        "A3": 4,
        "A4": 5,
        "A5": 6,
        "A6": 7,
        "A7": 8,
        "A8": 9
    }
}
```

### Versões de Modelo de Carro de Marca Determinada

Exemplo de chamada: `POST` https://apps.olx.com.br/autoupload/car_info/6/3 (no caso, o id `6` identifica a marca `AUDI` e o id `3` identifica o modelo `A3`, conforme exemplos acima):

Utilizando o cURL:

```bash
$ curl -A Mozila -L -X POST 'https://apps.olx.com.br/autoupload/car_info/6/3' -H 'Content-Type: application/json' --data-raw '{
    "access_token": "ca18abccaadd282490e75173f98b8ec6f0c1c6c8"
}'
```

Utilizando postman/insomnia:

```json
{
    "access_token": "ca18abccaadd282490e75173f98b8ec6f0c1c6c8"
}
```

Exemplo de retorno:

```json
{
    "status": "ok",
    "data": {
        "A1 1.4 TFSI 122CV S-TRONIC 3P": 1,
        "A1 SPORT 1.4 TFSI 185CV 3P S-TRONIC": 2,
        "A1 SPORTBACK 1.4 TFSI 185CV 5P S-TRONIC": 3,
        "A1 SPORTBACK 1.4 TFSI 5P S-TRONIC": 4,
        "A1 2.0 TFSI QUATTRO 256CV 3P": 5,
        "A1 SPORTBACK 1.8 TFSI 192CV 5P S-TRONIC": 6,
        "A1 SPORT. S EDITION 1.4 TFSI 5P S-TRONIC": 7
    }
}
```

## Motos

###  Marcas de Motos Disponíveis

Exemplo de chamada: `POST` https://apps.olx.com.br/autoupload/moto_info:

Utilizando o cURL:

```bash
$ curl -A Mozila -L -X POST 'https://apps.olx.com.br/autoupload/moto_info' -H 'Content-Type: application/json' --data-raw '{
    "access_token": "ca18abccaadd282490e75173f98b8ec6f0c1c6c8"
}'
```

Utilizando postman/insomnia:

```json
{
    "access_token":"ca18abccaadd282490e75173f98b8ec6f0c1c6c8"
}
```

Exemplo de retorno:

```json
{
    "status": "ok",
    "data": {
        "DUCATI": 1,
        "BUELL": 2,
        "KTM": 3,
        "KAHENA": 4,
        "FOX": 5,
        "MRX": 6,
        "YAMAHA": 7
    }
}
```


### Modelos de Motos de Determinada Marca

Exemplo de chamada: `POST` https://apps.olx.com.br/autoupload/moto_info/7 (no caso, o id `7` é a marca `YAMAHA`, conforme visto no exemplo acima):

Utilizando o cURL:

```bash
$ curl -A Mozila -L -X POST 'https://apps.olx.com.br/autoupload/moto_info/7' -H 'Content-Type: application/json' --data-raw '{
    "access_token": "ca18abccaadd282490e75173f98b8ec6f0c1c6c8"
}'
```

Utilizando postman/insomnia:

```json
{
    "access_token": "ca18abccaadd282490e75173f98b8ec6f0c1c6c8"
}
```

Exemplo de retorno: 

```json
{
    "status": "ok",
    "data": {
        "80": 2,
        "750": 1,
        "AXIS": 2,
        "BW'S": 3,
        "CRYPTON": 4,
        "DT": 5,
        "FAZER": 6
    }
}
```

### Versões de Modelo de Moto de Marca Determinada

Exemplo de chamada: `POST` https://apps.olx.com.br/autoupload/moto_info/7/6 (no caso, o id `7` identifica a marca `YAMAHA` e o id `6` identifica o modelo `FAZER`, conforme exemplos acima):

Utilizando o cURL:

```bash
$ curl -A Mozila -L -X POST 'https://apps.olx.com.br/autoupload/moto_info/7/6' -H 'Content-Type: application/json' --data-raw '{
    "access_token": "ca18abccaadd282490e75173f98b8ec6f0c1c6c8"
}'
```

Utilizando postman/insomnia:

```json
{
    "access_token": "ca18abccaadd282490e75173f98b8ec6f0c1c6c8"
}
```

Exemplo de retorno:

```json
{
    "status": "ok",
    "data": {
        "FAZER 600/ FZ6 S": 1
    }
}
```

### Cilindradas Disponíveis para Motos

Exemplo de chamada: `POST` https://apps.olx.com.br/autoupload/moto_cubiccms_info

Utilizando o cURL:

```bash
$ curl -A Mozila -L -X POST 'https://apps.olx.com.br/autoupload/moto_cubiccms_info' -H 'Content-Type: application/json' --data-raw '{
    "access_token": "ca18abccaadd282490e75173f98b8ec6f0c1c6c8"
}'
```

Utilizando postman/insomnia:

```json
{
    "access_token": "ca18abccaadd282490e75173f98b8ec6f0c1c6c8"
}
```

Exemplo de retorno:
```json
{
    "status": "ok",
    "data": {
        "1": "50",
        "2": "125",
        "3": "250",
        "4": "500",
        "5": "750",
        "6": "1000",
        "7": "150",
        "8": "200",
        "9": "300",
        "10": "350",
        "11": "400",
        "12": "450",
        "13": "550",
        "14": "600",
        "15": "650",
        "16": "700",
        "17": "800",
        "18": "850",
        "19": "900",
        "20": "950",
        "21": "Acima de 1.000",
        "22": "100"
    }
}
```
