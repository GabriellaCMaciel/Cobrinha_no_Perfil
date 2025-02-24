# Adicionando a Cobrinha ao Perfil do GitHub 🐍  
### Este tutorial ensina a adicionar uma animação de uma cobrinha "comendo" seus commits no perfil do GitHub. Isso é feito utilizando o GitHub Actions para gerar a imagem automaticamente e atualizá-la no seu README.  

## 📌 O que é essa cobrinha?
A cobrinha representa suas contribuições no GitHub de forma interativa. Ela percorre o gráfico de commits do seu perfil e os "come", criando uma animação dinâmica e divertida.

## 🛠️ Passo a passo para adicionar a cobrinha
### 1️⃣ Criar um repositório público com o nome igual ao seu usuário

Para que a cobrinha apareça no seu perfil, você precisa ter um repositório público chamado <seu-usuario>, por exemplo:

  Se seu usuário for devExemplo, o repositório deve ser devExemplo/devExemplo.  
Mas isso você já deve ter se já criou um README pro seu perfil.

1. Acesse o GitHub e vá para Repositórios.

2. Clique em `New` para criar um novo repositório.

4. No campo Repository name, digite exatamente o seu nome de usuário.

5. Marque a opção `Public.`

6. Clique em `Create repository.`

### 2️⃣ Criar o arquivo README.md

1. Dentro do repositório, crie um arquivo README.md (caso ainda não exista). Esse arquivo será o que exibe a cobrinha no seu perfil.

2. No repositório, clique em `Add file > Create new file`.

3. Nomeie o arquivo como `README.md`.

4. Dentro dele, adicione o seguinte código para exibir a cobrinha:

`![Snake animation](https://github.com/<seu-usuario>/<seu-usuario>/blob/output/github-contribution-grid-snake.svg)`

5. Substitua <seu-usuario> pelo seu nome de usuário.

6. Clique em `Commit new file`.

### 3️⃣ Criar a pasta .github/workflows

Agora vamos configurar o GitHub Actions para gerar a animação automaticamente:

1. No repositório, clique em `Add file > Create new file`.

2. Nomeie o arquivo como `.github/workflows/snake_game.yml.`

3. Adicione o seguinte código dentro dele:
````
name: Generate Snake Game

on:
  schedule:
    - cron: "0 0 * * *" 
  workflow_dispatch:

jobs:
  generate:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout do código
        uses: actions/checkout@v3

      - name: Gerar a animação da cobrinha
        uses: Platane/snk@v3
        with:
          github_user_name: ${{ github.repository_owner }}
          outputs: dist/github-contribution-grid-snake.svg

      - name: Commit e push da animação gerada
        run: |
          git config --local user.name "GitHub Actions"
          git config --local user.email "actions@github.com"
          git add dist/github-contribution-grid-snake.svg
          git commit -m "Add generated snake game GIF" || echo "Nenhuma mudança para commitar"
          git push
````
4. Clique em `Commit new file`.

### 4️⃣ Ativar o GitHub Actions

Após criar o workflow (snake_game.yml), o GitHub Actions será ativado automaticamente. Para verificar:

1. Vá até a aba Actions do seu repositório.

2. Confirme se o workflow Generate Snake Game está rodando.

3. Se der erro, verifique os logs e corrija conforme necessário.

### 5️⃣ Ver a cobrinha em ação!

Após a execução do GitHub Actions, a cobrinha será gerada e aparecerá no seu perfil dentro de alguns minutos. Para testar manualmente, vá até Actions e clique em Run workflow.

Caso não apareça, confira se o link da imagem no README.md está correto:

`![Snake animation](https://github.com/<seu-usuario>/<seu-usuario>/blob/output/github-contribution-grid-snake.svg)`

## 🔧 Solução de problemas

### ❌ A cobrinha não aparece no perfil

- Certifique-se de que o repositório é público.

- O nome do repositório deve ser exatamente igual ao seu usuário.

- O arquivo README.md deve conter o link correto da imagem.

- O workflow no GitHub Actions deve estar rodando corretamente.

### ❌ Erro de permissão no GitHub Actions (403)

- Vá até Settings > Actions e verifique se as permissões de escrita estão ativadas para GitHub Actions.

## 💡 Dica extra: Você pode personalizar as cores e o formato da imagem alterando os parâmetros no arquivo YAML!
A animação da cobrinha pode ser personalizada alterando os parâmetros no arquivo `snake_game.yml`. Você pode modificar:

✔ O formato da imagem (SVG, GIF, PNG)  
✔ As cores da cobrinha  
✔ As cores dos pontos (commits) no grid  
✔ O tema (claro ou escuro)  

### 📝 1️⃣ Alterando o Formato da Imagem
No código YAML do GitHub Actions, dentro da linha `outputs:`, você pode escolher entre três formatos:

- SVG (imagem vetorial, mais leve)
- GIF (imagem animada, mais dinâmica)
- PNG (imagem estática, mas colorida)

Exemplo no código:

```
outputs: |
  dist/github-snake.svg
  dist/github-snake.gif
  dist/github-snake.png
```
Se quiser apenas um formato, basta remover as outras linhas.

### 🌈 2️⃣ Alterando as Cores da Cobrinha e dos Pontos
Você pode modificar as cores da cobrinha e dos pontos do grid.

Adicionando cores personalizadas:

````
dist/github-snake.gif?color_snake=orange&color_dots=#8940e3,#7d36d6,#702cc8,#641fba,#5814ac
````

Aqui, cada parte tem um significado:

- `color_snake=orange` → Define a cor da cobrinha.
- `color_dots=#8940e3,#7d36d6,#702cc8,#641fba,#5814ac` → Define as cores dos pontos (commits) no gráfico.

Você pode usar qualquer código hexadecimal de cor para personalizar!

### 🌙 3️⃣ Alterando o Tema (Claro ou Escuro)
Se quiser que a cobrinha mude automaticamente com o tema do GitHub, use estas configurações:

````
outputs: |
  dist/github-snake.svg
  dist/github-snake-dark.svg?palette=github-dark
````

- O primeiro (`github-snake.svg`) será exibido no modo claro.
- O segundo (`github-snake-dark.svg`) será exibido no modo escuro.
Isso garante que a cobrinha fique visível corretamente em qualquer configuração de tema!

### 🎯 Como testar as cores antes de usar?
Se quiser testar combinações de cores antes de colocá-las no GitHub, pode usar sites como:
- [Color Hexa](https://www.colorhexa.com)
- [Coolors](https://coolors.co)

## 🎉 Pronto! Agora sua cobrinha está funcionando e personalizada!

Se você gostou desse tutorial, não se esqueça de dar uma ⭐ no repositório e compartilhar com outras pessoas. 🚀🐍
