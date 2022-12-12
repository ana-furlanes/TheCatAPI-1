# TheCatAPI

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
> Confira abaixo cada endpoint, suas formas de requisição e exemplos de _response body_. 🐾


**`POST / Images / Upload`**

Este endpoint **insere** uma nova imagem no sistema carregando um arquivo **válido** de imagem de gato, do tipo:

- .gif;
- .jpg;
- .png.

⚠️ O **file** é um _body param_ imprescindível. 


**Request body**

| Nome | Descrição | Tipo | Obrigatório |
|------|-----------|------|-------------|
| `file` | Arquivo em .gif, .png, ou .jpg | `file` | Sim |
| `sub_id` | ID para identificação interna. | `string` | Não |

### GET by ID

**Endpoint:** `GET /images/{image_id}`

Obtém a imagem correspondente ao parâmetro `image_id` passado como parâmetro `path`.

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
