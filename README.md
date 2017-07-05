![iPORTO](https://iporto.com.br/images/logos/64x64.png)

# Introdução a iPORTO e sua API

O objetivo desta documentação é orientar o desenvolvedor sobre como integrar com a **API iPORTO** o plano **Validador de Email**, 
descrevendo as funcionalidades, os métodos a serem utilizados, listando informações a serem enviadas e recebidas, e provendo exemplos.

O mecanismo de integração com o **Validador de Email** é simples, de modo que apenas conhecimentos intermediários em linguagem de programação para Web, 
requisições `HTTP/HTTPS` e manipulação de arquivos `JSON`, são necessários para implantar a solução **Validador de Email** com sucesso.

Nesse manual você encontrará a referência sobre todas as operações disponíveis na **API REST** da **API iPORTO**, para **Validador de Email**. 
Estas operações devem ser executadas utilizando sua **Chave de API**.

Não é preciso efetuar instalações adicionais para uso da **API iPORTO**.

## Recursos

 * Validação/Verificação de Email.
 * Validação de Email: Sintaxe.
 * Validação de Email: Domínios descartáveis.
 * Validação de Email: Usuários com digitação randômica.
 * Validação de Email: Domínios de instituições financeiras.
 * Validação de Email: Domínios de instituições governamentais.
 * Validação de Email: Domínios de uso gratuito.
 * Validação de Email: Usuários como Nome direto.
 * Validação de Email: Usuários de regra.
 * Validação de Email: Usuários como Trap ou Armadílhas.
 * Validação de Email: Usuários e Domínios conhecidos como Bounces ou Erros.
 * Validação de Email: Domínios como Typing Error.
 * Validação de Email: Domínios com contas Pega Tudo.
 * Validação de Email: Did You Mean ou seja, "Você quis dizer" para sugestões de digitação.
 * Validação de Email: MX.
 * Validação de Email: DNS.
 * Validação de Email: WEB.
 * Validação de Email: Análise de SPAM.
 * Validação de Email: Análise de Entregabilidade.
 * Validação de Email: Análise de Redes Sociais.

## Suporte

Após a leitura deste manual, caso ainda persistam dúvidas, a **iPORTO** disponibiliza um canal de suporte técnico de segunda a sexta-feira, em horário comercial, 
via Chamado Técnico em sua Central do Cliente:
 * [Central do Cliente](https://painel.iporto.com.br)

## Uso

Para utilização da API é preciso possuir um cadastro ativo na **iPORTO**. 
Um pacote de uso deve ser selecionado diretamente na página de planos disponíveis no site.
 * [Planos para Validador de Email](https://iporto.com.br/validador-de-email)

## Glossário

 * **iPORTO**: Empresa que provê solução para **Validador de Email**.
 * **Central do Cliente**: Ambiente de Cadastro na **iPORTO** para gerenciamento das **Chaves de API** e planos seleciondos.
 * **Chave de API**: Indica uma Chave única que deve ser gerada via **Central do Cliente**.
 * **Email**: Correio Eletrônico que será verificado de forma Online tendo como base regras definidas pela **iPORTO**.
 * **@todo**: Itens que serão disponibilizados no futuro mas que ainda não foram testados para uso final.

# Começar a usar

Acesse sua [Central do Cliente](https://painel.iporto.com.br/painel/api) e gere uma nova **Chave de API**. 
É preciso possuir uma Chave de API válida, um cadastro ativo e plano contratado.

## Limites
Cada **Chave de API** permite o limite de até `5.000` requisições ao dia. 
Para um uso maior, é preciso solicitar liberação através da **Central do Cliente**, que pode ser verificado na guia **Suporte**, desta documentação.

## EndPoint
Toda requisição tem como base:
 `https://api-v2.iporto.com.br/api-v2/`

## Requisição
Cada requisição, para **Validador de Email**, é composta de 2 parâmetros obrigatórios que são `@email` e `@iPORTO_Api_ChavePublica`. 
Todas as requisições devem ser feitas via `https`.

* Exemplo de requisição:
```curl
curl https://api-v2.iporto.com.br/api-v2/get/email/xx@domain.com/iPORTO_Api_ChavePublica/xx
```

## Resposta
Toda resposta da `API` utiliza padrão `REST`, neste caso, `RESTful JSON`.
* [Definição de REST via Wikipedia](https://pt.wikipedia.org/wiki/REST)
* [Especificações JSON para API](http://jsonapi.org/)

# Estrutura do Uso

A estrutura de uso tem como base `Request` e `Response`. 
`Request` indica o envio de dados para a `API` da **iPORTO** e `Response` indica a resposta com os dados formatados.

## Estrutura do `Request`
| Propriedade | Descrição
| ---: | :--- |
| `string` **iPORTO_Api_ChavePublica** | `Obrigatório`. **Chave de API** que será utilizada para autorizar a requisição.
|                   `string` **email** | `Obrigatório`. **Email** que será validado.

## Estrutura da `Response`
| Propriedade | Descrição |
| ---: | :--- |
|   `string` jsonapi | Versão atual da API.
|       `array` meta | Dados sobre a API.
|      `array` links | Links utilizados para `Request`.
|   `array` messages | Mensagens sobre `Request`.
|       `array` data | Itens retornados sobre `Request`. 

### Attributes
Disposição de atributos retornados para cada `Request`.

#### {meta}
| Array | Propriedade | Descrição |
| :---: | ---: | :--- |
| meta  | | |
|  `{}` | `string` email 		| Email que foi utilizado para validação.
|  `{}` | `string` domain 		| Domínio do Email que foi utilizado para validação.
|  `{}` | `string` tld 			| TLD do Domínio do Email que foi utilizado para validação.
|  `{}` | `string` subDomain 	| Subdomínio do Domínio do Email que foi utilizado para validação.
|  `{}` | `string` user 		| Usuário de Email.
|  `{}` | `string` emailMd5 	| Validação MD5 do Email que foi utilizado para validação.
|  `{}` | `string` emailSoundex | Validação SOUNDEX do Email que foi utilizado para validação. `@todo`

#### {diagnostic}
| Array | Propriedade | Descrição |
| :---: | ---: | :--- |
| diagnostic  | | |
|  `{}` | `string` key 	| Chave que identifica a requisição.
|  `{}` | `string` dts 	| Data, Hora, Minuto e Segundo em que a requisição foi iniciada.
|  `{}` | `string` dte 	| Data, Hora, Minuto e Segundo em que a requisição foi finalizada.
|  `{}` | `array` dtl 	| Histórico com Data, Hora, Minuto e Segundo de cada requisição principal.

#### {disposition}
| Array | Propriedade | Descrição |
| :---: | ---: | :--- |
| disposition  | | |
|  `{}` | `boolean` isValid 		| Informação de que um Email é realmente válido.
|  `{}` | `boolean` isValidFormat 	| Informação de que a sintax de um Email é válido.
|  `{}` | `boolean` isDisposable 	| Informação de que um Email utiliza serviços de Emails temporário e são descartáveis.
|  `{}` | `boolean` isGibberish 	| Informação de que um Email é do tipo Gibberish ou apenas um Email com digitação randômica.
|  `{}` | `boolean` isBank 			| Informação de que o Email é de uma instituição Bancária.
|  `{}` | `boolean` isGov 			| Informação de que o Email é de uma instituição Governamental. `@todo`
|  `{}` | `boolean` isFree 			| Informação de que o Email é gratuito.
|  `{}` | `boolean` isName 			| Informação de que o Usuário do Email é um Nome Próprio.
|  `{}` | `boolean` isRole 			| Informação de que o Email é do tipo Regra de entraga.
|  `{}` | `boolean` isTrap 			| Informação de que o Email é uma armadilha para capturar Spam.
|  `{}` | `boolean` isKnowError 	| Informação de que o Domínio é conhecido como diversos erros de envio.
|  `{}` | `boolean` isTypingError 	| Informação de que o Email ou o Domínio é um erro de digitação.
|  `{}` | `boolean` isCatchAll 		| Informação de que o Domínio aceita qualquer tipo de Email, inválido ou não. `@todo`

#### {didYouMean}
| Array | Propriedade | Descrição |
| :---: | ---: | :--- |
| didYouMean  | | |
|  `{}` | `array` didYouMean | `array` com sugestões de digitação. `@todo`

#### {emailVerification}
| Array | Array | Propriedade | Descrição |
| :---: | :--- | ---: | :--- |
| emailVerification | | | |
|  `{}` | `syntaxVerification` 	| `boolean` isSyntaxValid 			| Informação de que Email possui sintaxe válida.
|  `{}` | `dnsVerification` 	| `boolean` isDomainHasDnsRecord 	| Informação de que Domínio possui entrada de DNS.
|  `{}` | `dnsVerification` 	| `boolean` isDomainHasWebRecord 	| Informação de que Domínio possui entrada de DNS A/WEB.
|  `{}` | `dnsVerification` 	| `boolean` isDomainHasMxRecords 	| Informação de que Domínio possui entrada de DNS para Emails/MX.
|  `{}` | `dnsVerification` 	| `array` recordDns 				| Entradas de DNS para Domínio.
|  `{}` | `dnsVerification` 	| `array` recordWeb 				| Entradas de DNS para Domínios no âmbito Web.
|  `{}` | `dnsVerification` 	| `array` recordMx 					| Entradas de DNS para Domínios no âmbito de Emails. 
|  `{}` | `mailboxVerification` | `array` 							| Verificações de Email com análise Holística.

#### {infrastructure}
| Array | Array | Propriedade | Descrição |
| :---: | :--- | ---: | :--- |
| infrastructure  | | | |
|  `{}` | `mail` | `string` isSyntaxValid | Informação com estrutura de Email utilizada pelo Domínio. `@todo`

#### {sendAssess}
| Array | Propriedade | Descrição |
| :---: | ---: | :--- |
| sendAssess  | | |
|  `{}` | `int` inboxQualityScore 		| Verificação de qualidade para Mensagens sejam entregues na Caixa de Entrada dos Usuários.
|  `{}` | `string` sendRecommendation 	| Recomendação de que, se, um Email deve ser enviado ou não.
|  `{}` | `string` sendStatus 			| Status da última tentativa de envio para o Usário.

#### {spamAssess}
| Array | Propriedade | Descrição |
| :---: | :--- | :--- |
| spamAssess  | | |
|  `{}` | `array` | Análises, em resumo, para a chave `disposition`.

#### {social}
| Array | Propriedade | Descrição |
| :---: | :--- | :--- |
| social  | | |
|  `{}` | `array` | Análise com avatar e link para Rede Social do Usuário. `@todo`


### Exemplo de `Response` Json
```json
object(stdClass)#1 (7) {
  ["status"]=>
  int(200)
  ["jsonapi"]=>
  object(stdClass)#2 (1) {
    ["version"]=>
    string(5) "2.0.0"
  }
  ["meta"]=>
  object(stdClass)#3 (3) {
    ["copyright"]=>
    string(10) "iPORTO.COM"
    ["authors"]=>
    array(1) {
      [0]=>
      string(14) "api@iporto.com"
    }
    ["limits"]=>
    object(stdClass)#4 (1) {
      ["maxRequestsPerDay"]=>
      string(4) "5000"
    }
  }
  ["links"]=>
  array(1) {
    [0]=>
    string(99) "/api-v2/ve_data/get/email/xx@domain.com/iPORTO_Api_ChavePublica/xx"
  }
  ["errors"]=>
  NULL
  ["messages"]=>
  array(0) {
  }
  ["data"]=>
  object(stdClass)#5 (2) {
    ["count"]=>
    int(1)
    ["itens"]=>
    array(1) {
      [0]=>
      object(stdClass)#6 (3) {
        ["type"]=>
        string(5) "email"
        ["id"]=>
        NULL
        ["attributes"]=>
        object(stdClass)#7 (9) {
          ["meta"]=>
          object(stdClass)#8 (6) {
            ["email"]=>
            string(16) "xx@domain.com"
            ["domain"]=>
            string(10) "domain.com"
            ["tld"]=>
            string(3) "com"
            ["subDomain"]=>
            NULL
            ["user"]=>
            string(5) "xx"
            ["emailMd5"]=>
            string(32) "65ab4c7baf42aa70b74e8cb7887bd6b5"
          }
          ["diagnostic"]=>
          object(stdClass)#9 (4) {
            ["key"]=>
            string(32) "0f491c593a62b7fd875a68eef924e9a0"
            ["dts"]=>
            string(19) "2017-07-02 15:09:02"
            ["dte"]=>
            string(19) "2017-07-02 15:09:06"
            ["dtl"]=>
            array(7) {
              [0]=>
              array(2) {
                [0]=>
                string(18) "metaHeaderAnalytic"
                [1]=>
                string(19) "2017-07-02 15:09:02"
              }
              [1]=>
              array(2) {
                [0]=>
                string(28) "metaDispositionIsAllAnalytic"
                [1]=>
                string(19) "2017-07-02 15:09:02"
              }
              [2]=>
              array(2) {
                [0]=>
                string(29) "metaEmailVerificationAnalytic"
                [1]=>
                string(19) "2017-07-02 15:09:03"
              }
              [3]=>
              array(2) {
                [0]=>
                string(30) "metaDispositionIsValidAnalytic"
                [1]=>
                string(19) "2017-07-02 15:09:06"
              }
              [4]=>
              array(2) {
                [0]=>
                string(26) "metaInfrastructureAnalytic"
                [1]=>
                string(19) "2017-07-02 15:09:06"
              }
              [5]=>
              array(2) {
                [0]=>
                string(27) "metaSendAssessInboxAnalytic"
                [1]=>
                string(19) "2017-07-02 15:09:06"
              }
              [6]=>
              array(2) {
                [0]=>
                string(35) "metaSendAssessRecomendationAnalytic"
                [1]=>
                string(19) "2017-07-02 15:09:06"
              }
            }
          }
          ["disposition"]=>
          object(stdClass)#10 (12) {
            ["isValid"]=>
            bool(true)
            ["isValidFormat"]=>
            bool(true)
            ["isDisposable"]=>
            bool(false)
            ["isGibberish"]=>
            bool(false)
            ["isBank"]=>
            bool(false)
            ["isFree"]=>
            bool(false)
            ["isName"]=>
            bool(false)
            ["isRole"]=>
            bool(false)
            ["isTrap"]=>
            bool(false)
            ["isKnowError"]=>
            bool(false)
            ["isTypingError"]=>
            bool(false)
            ["isCatchAll"]=>
            bool(false)
          }
          ["didYouMean"]=>
          array(0) {
          }
          ["emailVerification"]=>
          object(stdClass)#11 (3) {
            ["syntaxVerification"]=>
            object(stdClass)#12 (1) {
              ["isSyntaxValid"]=>
              bool(true)
            }
            ["dnsVerification"]=>
            object(stdClass)#13 (6) {
              ["isDomainHasDnsRecord"]=>
              bool(true)
              ["isDomainHasWebRecord"]=>
              bool(true)
              ["isDomainHasMxRecords"]=>
              bool(true)
              ["recordDns"]=>
              array(2) {
                [0]=>
                object(stdClass)#14 (5) {
                  ["host"]=>
                  string(10) "domain.com"
                  ["class"]=>
                  string(2) "IN"
                  ["ttl"]=>
                  int(82358)
                  ["type"]=>
                  string(2) "NS"
                  ["target"]=>
                  string(22) "ns.domain.com"
                }
              }
              ["recordWeb"]=>
              array(1) {
                [0]=>
                object(stdClass)#16 (5) {
                  ["host"]=>
                  string(10) "domain.com"
                  ["class"]=>
                  string(2) "IN"
                  ["ttl"]=>
                  int(300)
                  ["type"]=>
                  string(1) "A"
                  ["ip"]=>
                  string(13) "192.168.0.1"
                }
              }
              ["recordMx"]=>
              array(5) {
                [0]=>
                object(stdClass)#17 (6) {
                  ["host"]=>
                  string(10) "domain.com"
                  ["class"]=>
                  string(2) "IN"
                  ["ttl"]=>
                  int(300)
                  ["type"]=>
                  string(2) "MX"
                  ["pri"]=>
                  int(10)
                  ["target"]=>
                  string(23) "mx.domain"
                }
              }
            }
            ["mailboxVerification"]=>
            array(1) {
              [0]=>
              object(stdClass)#22 (2) {
                ["result"]=>
                string(4) "Good"
                ["reason"]=>
                string(11) "ValidFormat"
              }
            }
          }
          ["infrastructure"]=>
          object(stdClass)#23 (1) {
            ["mail"]=>
            array(1) {
              [0]=>
              NULL
            }
          }
          ["sendAssess"]=>
          object(stdClass)#24 (3) {
            ["inboxQualityScore"]=>
            int(100)
            ["sendRecommendation"]=>
            string(3) "Yes"
            ["sendStatus"]=>
            string(70) "200%200.0.0%20No%20connections%20was%20made"
          }
          ["spamAssess"]=>
          object(stdClass)#25 (10) {
            ["isDisposable"]=>
            bool(false)
            ["isGibberish"]=>
            bool(false)
            ["isBank"]=>
            bool(false)
            ["isFree"]=>
            bool(false)
            ["isName"]=>
            bool(false)
            ["isRole"]=>
            bool(false)
            ["isTrap"]=>
            bool(false)
            ["isKnowError"]=>
            bool(false)
            ["isTypingError"]=>
            bool(false)
            ["isCatchAll"]=>
            bool(false)
          }
          ["social"]=>
          array(1) {
            [0]=>
            NULL
          }
        }
      }
    }
  }
}
```

# Exemplos de Uso

Para utilizar a chamada de `API` é preciso apenas efetuar uma requisição `HTTPS`. 
Toda linguagem de programação que permite uma requisição `HTTPS` pode ser utilizada.
Todos os exemplos utilizarão a `variável` `@endpoint`, para uso, é preciso alterar esta variável por sua requisição final, 
tendo atenção a regra básica para os parâmetros necessários que são `@email` e  `@iPORTO_Api_ChavePublica`

 * [Gerar Chave de API iPORTO](http://painel.iporto.com.br/painel/api)
 * [Contratar Plano Validador de Email](https://iporto.com.br/validador-de-email)


```
@endpoint = "https://api-v2.iporto.com.br/api-v2/get/email/xx@domain.com/iPORTO_Api_ChavePublica/xx";
```

### Curl
```curl
curl @endpoint
```

### Php
```php
<?php
$get_json = file_get_contents(@endpoint);
```

### Javascript com jQuery
```javascript
$.getJSON(@endpoint, function(data) {
  get_json = data;
});
```

### Ruby
```ruby
require "open-uri"
get_json = open(@endpoint).read
```

### Asp Clássico
```asp
<%
Set xmlHttp = Server.Createobject("MSXML2.ServerXMLHTTP.6.0") 
xmlHttp.Open "GET", @endpoint, False 
xmlHttp.Send 
_RESTfulResponse = xmlHttp.responseText 
xmlHttp.abort() 
set xmlHttp = Nothing 
get_json = _RESTfulResponse 
```

# Contrato
@iPORTO.COM - suporte[]iporto.com

* [Contrado de API](https://iporto.com.br/contratos/api.pdf)