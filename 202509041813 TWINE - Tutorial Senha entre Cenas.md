---
title: "Guia Prático: Sistema de Senha com Tentativas no Twine"
tags:
  - Twine
  - Harlowe
  - Tutorial
  - Lógica-Programação
  - Narração-Não-Linear
Comentários:
  - Aprenda a criar um sistema de senha com tentativas limitadas no Twine usando o formato Harlowe. Este tutorial detalha a estrutura de código e a lógica de passagens para construir um desafio robusto, ideal para iniciantes em jogos narrativos.
Data: 2025-09-04T18:13:00
Autores: Humberto Luz Oliveira
---
## Tutorial Twine: Criando um Desafio de Senha com Tentativas Limitadas

Olá! Aqui é o Professor Humberto Luz Oliveira (Humb@).

Uma das mecânicas mais clássicas em jogos e histórias interativas é a boa e velha porta trancada que precisa de uma senha. É um ótimo quebra-cabeça para iniciantes, pois nos ensina os três pilares de uma história dinâmica no Twine (especificamente no formato Harlowe):

1. **Lembrar de coisas:** Usando variáveis para guardar informações, como a senha correta e quantas tentativas o jogador ainda tem.
    
2. **Receber informações do jogador:** Capturando a senha que o jogador digita.
    
3. **Tomar decisões:** Verificando se a senha está correta e decidindo o que acontece a seguir.
    

Neste tutorial, vamos construir juntos, passo a passo, um sistema de senha robusto e reutilizável. Veremos não apenas _o que_ o código faz, mas _por que_ ele é estruturado dessa maneira.

### A Filosofia: Separar a "Preparação" da "Ação"

O erro mais comum ao criar um sistema como este é misturar o código que _inicia_ o quebra-cabeça com o código que _executa_ o quebra-cabeça. Isso leva a um loop onde as tentativas do jogador são reiniciadas a cada erro.

Para evitar isso, usaremos uma **estrutura de três passagens**:

1. **A Passagem de Setup (`Inicio do Jogo`):** Prepara o cenário. Ela define as variáveis e é vista **apenas uma vez**.
    
2. **A Passagem de Interação (`Porta Misteriosa`):** É o "hub" do desafio. É aqui que o jogador fica enquanto tenta resolver o quebra-cabeça.
    
3. **A Passagem de Lógica (`Verifique Senha`):** O "cérebro" da operação. Ela processa a entrada do jogador e redireciona o fluxo da história.
    

Vamos ao código.

### Passo 1: A Passagem de Setup

Esta é a porta de entrada para o nosso quebra-cabeça. Sua única função é definir as variáveis iniciais e mover o jogador para a cena de ação.

**Nome da Passagem:** `Inicio do Jogo`

```
:: Inicio do Jogo

<!-- Esta passagem roda apenas uma vez para configurar o desafio. -->

<!-- 1. Definimos a senha correta. Usamos 'to' para atribuir o valor. -->
(set: $senha_correta to "albedo")

<!-- 2. Definimos o número inicial de tentativas. -->
(set: $tentativas to 2)

Bem-vindo ao jogo! Você encontrou uma porta misteriosa. Para abri-la, precisa de uma senha secreta.

<!-- 3. Usamos (goto:) para enviar o jogador para a próxima passagem
imediatamente, sem precisar de um clique. -->
(goto: "Porta Misteriosa")
```

### Passo 2: A Passagem de Interação (O Hub)

Esta é a cena principal do quebra-cabeça. O jogador retornará aqui toda vez que errar a senha (contanto que ainda tenha tentativas). O importante é que esta passagem **não redefine nenhuma variável**, apenas exibe o estado atual delas.

**Nome da Passagem:** `Porta Misteriosa`

```
:: Porta Misteriosa

Você está diante da porta misteriosa.

<!-- Apenas exibimos o valor atual da variável $tentativas. -->
Você tem $tentativas tentativa(s) restante(s).

<!--
A macro (link:) cria um texto clicável. O código dentro do seu
hook [] só é executado quando o jogador clica.
-->
(link: "Tentar digitar a senha")[
    
    <!--
    A macro (prompt:) abre uma janela pop-up pedindo uma entrada de texto.
    O que o jogador digita é então guardado na variável $senha_digitada.
    O segundo valor ("") é o texto padrão que aparece na caixa de texto.
    -->
    (set: $senha_digitada to (prompt: "Qual é a senha?", ""))
    
    <!-- Após o jogador digitar, o levamos para a passagem de lógica. -->
    (goto: "Verifique Senha")
]
```

### Passo 3: A Passagem de Lógica (O Cérebro)

Esta passagem é invisível para o jogador no sentido de que ela não contém uma "cena". Sua única função é receber a `$senha_digitada`, compará-la, atualizar o estado do jogo e redirecionar o jogador para o resultado apropriado.

**Nome da Passagem:** `Verifique Senha`

```
:: Verifique Senha

<!-- 1. Verificamos se a senha digitada é igual à senha correta. -->
(if: $senha_digitada is $senha_correta)[

    <!-- Se for, o jogador venceu. Mostramos uma mensagem e um link para avançar. -->
    Parabéns! Você acertou a senha secreta!
    [[Fase 2 - Segredo Revelado]]

](else:)[ <!-- Se a senha estiver errada... -->

    <!-- Primeiro, diminuímos o número de tentativas. -->
    (set: $tentativas to $tentativas - 1)

    <!-- 2. Agora, verificamos se o jogador ainda tem tentativas restantes. -->
    (if: $tentativas > 0)[
    
        <!-- Se sim, informamos o erro e o levamos de volta ao Hub. -->
        A senha ''$senha_digitada'' está incorreta. Você ainda tem $tentativas tentativa(s) restante(s).
        [[Tentar Novamente->Porta Misteriosa]]

    ](else:)[ <!-- Se as tentativas acabaram... -->
    
        <!-- Fim de jogo. O jogador falhou. Damos a ele a opção de recomeçar. -->
        Você esgotou todas as suas tentativas. A porta se fecha, e você é teletransportado de volta para o início.
        [[Voltar ao Início->Inicio do Jogo]]
    ]
]
```

### Resumo do Fluxo da História

Se fôssemos desenhar o caminho do jogador, ele se pareceria com isto:

1. **`Inicio do Jogo`** -> (configura variáveis) -> **`Porta Misteriosa`**
    
2. **`Porta Misteriosa`** -> (jogador clica e digita) -> **`Verifique Senha`**
    
3. **`Verifique Senha`** pode levar a três lugares:
    
    - **Sucesso:** -> `Fase 2 - Segredo Revelado`
        
    - **Erro (com tentativas):** -> `Porta Misteriosa` (para tentar de novo)
        
    - **Falha (sem tentativas):** -> `Inicio do Jogo` (para recomeçar)
        

Espero que esta documentação detalhada ajude outros criadores a entender a "magia" por trás da lógica do Harlowe. É um sistema poderoso uma vez que você pega o jeito de separar as responsabilidades de cada passagem.

Continue criando!

— Humberto Luz Oliveira (Humb@)