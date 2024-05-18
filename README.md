# Documentação da API Gamero Gaming

## Visão Geral

A API Gamero Gaming fornece acesso aos dados dos usuários registrados em nossa plataforma. Atualmente, a API oferece suporte para recuperar os seguintes dados de um usuário:

- Nome do usuário
- Steam
- Epic Games

## Uso da API

### Endpoint

O endpoint principal da API é:

```
https://gg.gamerocorporation.com/api.php
```

### Requisição

Para recuperar os dados de um usuário específico, você precisa fazer uma solicitação GET para o endpoint da API, fornecendo o username do usuário desejado como parâmetro na URL.

```
https://gg.gamerocorporation.com/api.php?username=exampleuser
```

Substitua `exampleuser` pelo username do usuário que deseja consultar.

### Resposta

A API responderá com os dados do usuário em formato JSON. Aqui está um exemplo de resposta:

```json
{
  "nome_usuario": "exampleuser",
  "steam": "steamid123456",
  "epicgames": null
}
```

- **nome_usuario**: O nome de usuário do usuário consultado.
- **steam**: O Username da conta Steam associado ao usuário, se disponível. Se não houver uma conta Steam associada, o valor será `null`.
- **epicgames**: O Username da conta Epic Games associado ao usuário, se disponível. Se não houver uma conta Epic Games associada, o valor será `null`.

Se o usuário consultado não for encontrado, a API responderá com uma mensagem de erro.

### Exemplo de Uso (JavaScript)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Dados do Usuário</title>
</head>
<body>
    <div id="user-data"></div>

    <script>
        const username = 'exampleuser'; // Altere para o username que deseja consultar

        fetch(`https://gg.gamerocorporation.com/api.php?username=${username}`)
            .then(response => response.json())
            .then(data => {
                const userDataDiv = document.getElementById('user-data');
                if (data.message) {
                    userDataDiv.textContent = data.message;
                } else {
                    userDataDiv.innerHTML = `
                        <p>Username: ${data.nome_usuario}</p>
                        <p>Steam: ${data.steam !== null ? data.steam : 'N/A'}</p>
                        <p>Epic Games: ${data.epicgames !== null ? data.epicgames : 'N/A'}</p>
                    `;
                }
            })
            .catch(error => console.error('Error:', error));
    </script>
</body>
</html>
```

Este é um exemplo simples de como usar a API em uma página da web para exibir os dados do usuário.
