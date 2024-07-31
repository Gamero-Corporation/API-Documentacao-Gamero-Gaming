### Documentação para Jogos disponíveis para Jogar

#### Visão Geral

A API Gamero Gaming fornece acesso aos jogos disponíveis para jogar na plataforma. Atualmente, a API oferece suporte para recuperar os seguintes dados de um jogo para jogar na plantaforma:

- Nome do item
- PEGI
- Data de lançamento
- Categoria

#### Uso da API

##### Endpoint

O endpoint principal da API para jogos disponíveis para jogar é o mesmo da API de dados do usuário:

```
https://gg.gamerocorporation.com/api2.php
```

##### Requisição

Para recuperar todos os jogos disponíveis para jogar, você precisa fazer uma solicitação GET para o endpoint da API, incluindo o parâmetro `getplaygame` e um `token` válido como parâmetro na URL.

```
https://gg.gamerocorporation.com/api2.php?getplaygame&token=yourtoken
```

Substitua `yourtoken` pelo token de acesso.

##### Resposta

A API responderá com os dados dos jogos disponíveis para jogar em formato JSON. Aqui está um exemplo de resposta:

```json
[
  {
    "nome": "Jogo 1",
    "pegi": 18,
    "lancamento": "2024-05-19",
    "categoria": "Categoria A"
  },
  {
    "nome": "Jogo 2",
    "pegi": 13,
    "lancamento": "2024-05-19",
    "categoria": "Categoria B"
  }
]
```

Cada objeto representa um item da loja e inclui os seguintes campos:
- **nome**: O nome do jogo.
- **pegi**: A classificação recomendada.
- **lancamento**: A data de lançamento do jogo.
- **categoria**: A categoria à qual o jogo pertence.

##### Exemplo de Uso (JavaScript)

```<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Jogos disponíveis para jogar</title>
</head>
<body>
    <div id="gaming-play"></div>

    <script>
        fetch('https://gg.gamerocorporation.com/api2.php?getplaygame&token=yourtoken')
            .then(response => response.json())
            .then(data => {
                const gamingPlayDiv = document.getElementById('gaming-play');
                
                // Verificar se a resposta é um objeto com as propriedades esperadas
                if (data && data.nome && data.pegi && data.lancamento && data.categoria) {
                    const gameDiv = document.createElement('div');
                    gameDiv.innerHTML = `
                        <p>Nome: ${data.nome}</p>
                        <p>PEGI: ${data.pegi}</p>
                        <p>Data de Lançamento: ${data.lancamento}</p>
                        <p>Categoria: ${data.categoria}</p>
                        <hr>
                    `;
                    gamingPlayDiv.appendChild(gameDiv);
                } else {
                    gamingPlayDiv.textContent = 'Nenhum jogo encontrado.';
                }
            })
            .catch(error => console.error('Erro:', error));
    </script>
</body>
</html>
```

#### Mensagens de Erro

A API pode responder com mensagens de erro semelhantes às da API de dados do usuário, caso ocorram problemas durante a solicitação.
