### Documentação para Itens da Loja

#### Visão Geral

A API Gamero Gaming fornece acesso aos itens disponíveis na loja da plataforma. Atualmente, a API oferece suporte para recuperar os seguintes dados de um item da loja:

- Nome do item
- Categoria
- Data de lançamento
- Preço

#### Uso da API

##### Endpoint

O endpoint principal da API para itens da loja é o mesmo da API de dados do usuário:

```
https://gg.gamerocorporation.com/api2.php
```

##### Requisição

Para recuperar todos os itens disponíveis na loja, você precisa fazer uma solicitação GET para o endpoint da API, incluindo o parâmetro `getitensstore` e um `token` válido como parâmetro na URL.

```
https://gg.gamerocorporation.com/api2.php?getitensstore&token=yourtoken
```

Substitua `yourtoken` pelo token de acesso.

##### Resposta

A API responderá com os dados dos itens da loja em formato JSON. Aqui está um exemplo de resposta:

```json
[
  {
    "nome": "Item 1",
    "categoria": "Categoria A",
    "data_lancamento": "2024-05-19",
    "preco": 10.99
  },
  {
    "nome": "Item 2",
    "categoria": "Categoria B",
    "data_lancamento": "2024-05-18",
    "preco": 19.99
  }
]
```

Cada objeto representa um item da loja e inclui os seguintes campos:
- **nome**: O nome do item.
- **categoria**: A categoria à qual o item pertence.
- **data_lancamento**: A data de lançamento do item.
- **preco**: O preço do item.

##### Exemplo de Uso (JavaScript)

```<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Itens da Loja</title>
</head>
<body>
    <div id="store-items"></div>

    <script>
        fetch('https://gg.gamerocorporation.com/api2.php?getitensstore&token=yourtoken')
            .then(response => response.json())
            .then(data => {
                const storeItemsDiv = document.getElementById('store-items');
                if (Array.isArray(data) && data.length > 0) {
                    data.forEach(item => {
                        const itemDiv = document.createElement('div');
                        itemDiv.innerHTML = `
                            <p>Nome: ${item.nome}</p>
                            <p>Categoria: ${item.categoria}</p>
                            <p>Data de Lançamento: ${item.data_lancamento}</p>
                            <p>Preço: $${item.preco.toFixed(2)}</p>
                            <hr>
                        `;
                        storeItemsDiv.appendChild(itemDiv);
                    });
                } else {
                    storeItemsDiv.textContent = 'Nenhum item encontrado.';
                }
            })
            .catch(error => console.error('Erro:', error));
    </script>
</body>
</html>
```

#### Mensagens de Erro

A API pode responder com mensagens de erro semelhantes às da API de dados do usuário, caso ocorram problemas durante a solicitação.
