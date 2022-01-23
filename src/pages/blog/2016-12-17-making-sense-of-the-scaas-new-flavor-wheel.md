---
templateKey: blog-post
title: Como remover espaços em branco de uma String
date: 2022-01-23T12:42:26.675Z
description: Existem algumas maneiras e cenários em que isso pode ser aplicado,
  por exemplo na validações de campos de senha, nome, email ou alguma outra
  coisa.
featuredpost: false
featuredimage: /img/imagem-post-remover-espaço-em-branco.png
tags:
  - JavaScript
---
![](/img/imagem-post-remover-espaço-em-branco.png)

Vou deixar no final desse post a função pronta para quem deseja usar ela, recomendo ler o post todo para entender como as coisas foram feitas para chegar nesse resultado.

Se a validação tiver que ser feita enquanto o usuário digita podemos utilizar do evento **keyup** direto no input.

## Removendo espaço em branco ao digitar:

Primeiramente temos que criar um input e adicionar o evento **keyup** nele. Se a validação for feita quando o usuário sai do campo é só substituir o evento **keyup** por um evento **blur.**

![<span id="error-message" style="color: red;"></span> <input id='my-input' onkeyup="verifyCharacter(this.value)">](/img/carbon-2-.png "Input")

Eu aproveitei e já criei um **span** para apresentar a mensagem de erro.

Agora que já temos um campo de entrada para nosso texto, podemos fazer uma função para receber tudo que é digitado no input, dessa forma a cada caractere digitado podemos verificar se é um espaço em branco ou não.

![](/img/cria-função-valida-caracteres.png "Função que valida espaço em branco.")

Essa função deve receber o valor do input como parâmetro.

Agora que já recebemos o valor do input podemos verificar se existe espaço em branco.

![](/img/valida-espaço-em-branco.png "Verifica se tem espaço em branco.")

Com essa validação a constante **hasWhiteSpace** vai receber um valor quando existir espaço vazio dentro do input e quando não existir nenhum espaço em branco, ela não recebe nada. Agora podemos remover esse espaço em branco e fazer as tratativas.

![](/img/remove-espaço-em-branco.png "Remove espaço em branco e faz tratativas.")

Pronto, dessa forma sempre que o usuário digitar um espaço em branco a função ***.trim()*** remove e apresenta uma mensagem de aviso para o usuário.

Resultado:

```javascript
/**
* Função responsável por verificar caracteres.
**/
const verifyCharacter = (inputValue) => {
    
  /**
  * Verifica se a senha atual tem espaço em branco.
  */
  const hasWhiteSpace = inputValue.indexOf(' ') >= 0;
    
  if (hasWhiteSpace) {
    document.querySelector("#error-message").innerHTML = "Senha não pode conter espaço em branco."
    
    /**
    * Pega o input correto.
    **/
    const input = document.querySelector("#my-input");
    
    /**
    * Remove o espaço em branco.
    **/
    input.value = inputValue.trim()
    return
  }
    
  /**
  * Remove mensagem de erro.
  **/
  document.querySelector("#error-message").innerHTML = ""
}
```