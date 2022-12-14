# TheCatAPI-DOC

>
> The Cat API é uma API pública de **gerenciamento de informações** e **imagens de gatos**, para deixar o dia mais alegre. 🐈

Com a The Cat API, é possível: 

1. **Gerar** imagens;
2. **Buscar** imagens por ID;
3. **Excluir** imagens.

⚠️ _Imagens que não forem de gatos ou inapropriadas são rejeitadas_. O objeto `images` representa as fotos de gatos enviadas.

## Pré-requisitos

- Faça o registro em [https://thecatapi.com/signup](https://thecatapi.com/signup) para receber sua API key por email.
- Informe a API key no header das chamadas através da variável `x-api-key`.
- Utilize nas chamadas o path [https://api.thecatapi.com/v1](https://api.thecatapi.com/v1).

## Endpoints

>
> Confira abaixo cada endpoint, suas formas de requisição e exemplos de _response body_. 


🐱 **`POST / Images / Upload`** `https://api.thecatapi.com/v1/images/upload`

Este endpoint **insere** uma nova imagem no sistema carregando um arquivo **válido** de imagem de gato, do tipo:

- .gif
- .jpg
- .png

**Request body**

| Nome | Descrição | Tipo | Obrigatório |
|------|-----------|------|-------------|
| `file` | Arquivo em .gif, .png, ou .jpg | `file` | Sim |
| `sub_id` | ID para identificação interna. | `string` | Não |


**Exemplo de requisição:** 

```
curl --location --request POST 'https://api.thecatapi.com/v1/images/upload' \
--header 'x-api-key: live_g6EUZSGbkMsKSuQm1OyWDVeLrLSnoCMcps2f7BMcDq6Alt2Y9Z606aj1uF6sPF35' \
--form 'file=@"iQzJdW8Ds/Mia.jpg"'
```

![Mia](https://user-images.githubusercontent.com/105396649/207432035-c638a387-f243-4983-8af5-fcf7e0c94011.jpg)

😻 A resposta de código `201 Created` indica que o registro da imagem foi criado com sucesso. Retorna um JSON com as informações, incluindo o novo ID.

**Exemplo positivo de _response body_:**

``` json
{
    "id": "RyOzgrhxk",    
    "url": "https://cdn2.thecatapi.com/images/RyOzgrhxk.jpg",   
    "width": 1047,    
    "height": 647,    
    "original_filename": "Mia.jpg",    
    "pending": 0,    
    "approved": 1  
}
```

**Exemplos negativos de _response body_:**

-  `400 Bad request` Invalid file data. Check you are sending the formdata.append('file', ...} format'
> Response type: application/JSON

-  `400 Bad request` Classifcation failed: correct animal found. 
> Response type: application/JSON

-  `401 Unauthorized` Unauthorized
> Response type: application/text

-  `500 Internal Server Error` Internal Server Error. 
> Response type: application/text

### GET by ID

🐱 **`GET /images/{image_id}`** `https://api.thecatapi.com/v1/images/{{image_id}}`

Este endpoint **busca** a imagem correspondente ao **_path param_** `image_id`.

**Exemplo de requisição:** 

```
curl --location --request GET 'https://api.thecatapi.com/v1/images/6qmirugX0' \
--header 'x-api-key: live_g6EUZSGbkMsKSuQm1OyWDVeLrLSnoCMcps2f7BMcDq6Alt2Y9Z606aj1uF6sPF35'
```

![Mia2](https://user-images.githubusercontent.com/105396649/207641262-48edba35-f423-4835-84ce-7f9109237485.jpg)

😻 A resposta de código `200 OK` indica que a consulta foi executada com sucesso. Ela retorna um JSON com todas as informações da imagem.

**Exemplo positivo de _response body_:**

``` json

{
    "id": "6qmirugX0",
    "url": "https://cdn2.thecatapi.com/images/6qmirugX0.jpg",
    "width": 1047,
    "height": 647,
    "sub_id": null
}

```

### GET

**Endpoint:** `GET /images`

Obtenha todas as imagens enviadas para sua conta via `/images/upload`. Os resultados podem ser filtrados através dos parâmteros `query` abaixo:

| Parâmetro |    Descrição      | Tipo | Obrigatório |
|------------|--------------------|------|------------|
| `limit`  | Número de resultados a serem retornados. O valor máximo é 25. O padrão é 1. | `integer` | Sim |
| `mime_types` | Os tipos de imagem a serem retornados: .gif, .jpg, ou .png. Retorna todos os tipos como padrão. | `string` delimitado por vírgulas. | Não |
| `order` | A ordem de retorno: RANDOM, ASC ou DESC. O padrão é RANDOM. | `string` | Não  |

### DELETE

**Endpoint:** `DELETE /images/{image_id}`

Exclui a imagem correspondente ao parâmetro `image_id` passado como parâmetro `path`.
