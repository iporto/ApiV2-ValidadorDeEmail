![iPORTO](https://iporto.com.br/images/logos/64x64.png)

VALIDADOR DE E-MAIL
=======

# API

O objetivo desta documentação é orientar o desenvolvedor sobre como integrar com a **API iPORTO** o plano **Validador de E-mail**, 
descrevendo as funcionalidades, os métodos a serem utilizados, listando informações a serem enviadas e recebidas, e provendo exemplos.

O mecanismo de integração com o Validador de E-mail é simples, de modo que apenas conhecimentos intermediários em linguagem de programação para Web, 
requisições HTTP/HTTPS e manipulação de arquivos JSON, são necessários para implantar a solução Validador de E-mail com sucesso.

Nesse manual você encontrará a referência sobre todas as operações disponíveis na API REST da API iPORTO, para Validador de E-mail. 
Estas operações devem ser executadas utilizando sua chave de API (iPORTO_Api_ChavePublica).

*Current version: [v2.0.0][stable]*

## Recursos

    * Validação/Verificação de E-mail.
    * Validação de E-mail: Sintaxe.
    * Validação de E-mail: Domínios descartáveis.
    * Validação de E-mail: Usuários com digitação randômica.
    * Validação de E-mail: Domínios de instituições financeiras.
    * Validação de E-mail: Domínios de instituições governamentais.
    * Validação de E-mail: Domínios de uso gratuito.
    * Validação de E-mail: Usuários como Nome direto.
    * Validação de E-mail: Usuários de regra.
    * Validação de E-mail: Usuários como Trap ou Armadílhas.
    * Validação de E-mail: Usuários e Domínios conhecidos como Bounces ou Erros.
    * Validação de E-mail: Domínios como Typing Error.
    * Validação de E-mail: Domínios com contas Pega Tudo.
    * Validação de E-mail: Did You Mean ou seja, "Você quis dizer" para sugestões de digitação.
    * Validação de E-mail: MX.
    * Validação de E-mail: DNS.
    * Validação de E-mail: WEB.
    * Validação de E-mail: Análise de SPAM.
    * Validação de E-mail: Análise de Entregabilidade.
    * Validação de E-mail: Análise de Redes Sociais.

## Suporte
Após a leitura deste manual, caso ainda persistam dúvidas, a **iPORTO** disponibiliza um canal de suporte técnico de segunda a sexta-feira, em horário comercial, 
via Chamado Técnico em sua Central do Cliente:
* [Central do Cliente](https://painel.iporto.com.br)

## Uso
Para utilização da API é preciso possuir um cadastro ativo na **iPORTO**. 
Um pacote de uso deve ser selecionado diretamente na página de planos disponíveis no site.
* [Planos para Validador de E-mail](https://iporto.com.br/validador-de-email)

## Glossário

    * Chave de API: Indica uma Chave única que deve ser gerada via Central do Cliente para uso da API e requisições.
    * Email: Correio Eletrônico que será verificado de forma Online tendo como base regras definidas pela **iPORTO**.
    * Central do Cliente: Ambiente de Cadastro na **iPORTO** para gerenciamento das **Chaves de API** e planos seleciondos.

# Começar a usar

Acesse sua [Central do Cliente](https://painel.iporto.com.br/painel/api) e gere uma nova **Chave de API**. 
É preciso possuir uma Chave de API válida, um cadastro ativo e plano contratado.

## Limites
Cada **Chave de API** permite o limite de até 5.000 requisições ao dia. 
Para um uso maior, é preciso solicitar liberação através da Central do Cliente, que pode ser verificado na guia Suporte desta documentação.

## EndPoint
Toda requisição tem como base:
 `https://api-v2.iporto.com.br/api-v2/`

## Requisição
Cada requisição, para Validador de E-mail, é composta de 2 parâmetros obrigatórios que são `@email` e `@iPORTO_Api_ChavePublica`. 
Todas as requisições devem ser feitas via `https`.

* Exemplo de requisição:
```curl
curl https://api-v2.iporto.com.br/api-v2/get/email/xx@domain.com/iPORTO_Api_ChavePublica/xx
```

## Resposta
Toda resposta da API utiliza padrão `REST`, neste caso, `RESTful JSON`.
* [Definição de REST via Wikipedia](https://pt.wikipedia.org/wiki/REST)
* [Especificações JSON para API](http://jsonapi.org/)


# Estrutura do Uso

| Propriedade | Descrição
| ---: | :--- |
| `string` **iPORTO_Api_ChavePublica** | `Obrigatório`. Chave de API que será utilizada para autorizar a requisição.
|                   `string` **email** | `Obrigatório`. E-mail que será validado.

# Estrutura da Resposta

| Propriedade | Descrição |
| ---: | :--- |
|   jsonapi | Versão atual da API.
|      meta | Dados sobre a API.
|     links | Links utilizados para a requisição.
|  messages | Mensagens sobre a requisição.
|      data | Itens retornados sobre a requisição. 

### Attributes
Disposição de atributos retornados para cada requisição.

#### meta
| Array | Propriedade | Descrição |
| :---: | :---: | :--- |
| meta  | | |
|  `{}` | `string` email 		| E-mail que foi utilizado para validação.
|  `{}` | `string` domain 		| Domínio do E-mail que foi utilizado para validação.
|  `{}` | `string` tld 			| TLD do Domínio do E-mail que foi utilizado para validação.
|  `{}` | `string` subDomain 	| Subdomínio do Domínio do E-mail que foi utilizado para validação.
|  `{}` | `string` user 		| Usuário de E-mail.
|  `{}` | `string` emailMd5 	| Validação MD5 do E-mail que foi utilizado para validação.

#### diagnostic
| Array | Propriedade | Descrição |
|--|--|--|
| diagnostic  | | |
|  `{}` | `string` key 	| Chave que identifica a requisição.
|  `{}` | `string` dts 	| Data, Hora, Minuto e Segundo em que a requisição foi iniciada.
|  `{}` | `string` dte 	| Data, Hora, Minuto e Segundo em que a requisição foi finalizada.
|  `{}` | `array` dtl 	| Histórico com Data, Hora, Minuto e Segundo de cada requisição principal.

#### disposition
| Array | Propriedade | Descrição |
|--|--|--|
| disposition  | | |
|  `{}` | `boolean` isValid 		| Informação de que um E-mail é realmente válido.
|  `{}` | `boolean` isValidFormat 	| Informação de que a sintax de um E-mail é válido.
|  `{}` | `boolean` isDisposable 	| Informação de que um E-mail utiliza serviços de E-mails temporário e são descartáveis.
|  `{}` | `boolean` isGibberish 	| Informação de que um E-mail é do tipo Gibberish ou apenas um E-mail com digitação randômica.
|  `{}` | `boolean` isBank 			| Informação de que o E-mail é de uma instituição Bancária.
|  `{}` | `boolean` isGov 			| Informação de que o E-mail é de uma instituição Governamental.
|  `{}` | `boolean` isFree 			| Informação de que o E-mail é gratuito.
|  `{}` | `boolean` isName 			| Informação de que o Usuário do E-mail é um Nome Próprio.
|  `{}` | `boolean` isRole 			| Informação de que o E-mail é do tipo Regra de entraga.
|  `{}` | `boolean` isTrap 			| Informação de que o E-mail é uma armadilha para capturar Spam.
|  `{}` | `boolean` isKnowError 	| Informação de que o Domínio é conhecido como diversos erros de envio.
|  `{}` | `boolean` isTypingError 	| Informação de que o E-mail ou o Domínio é um erro de digitação.
|  `{}` | `boolean` isCatchAll 		| Informação de que o Domínio aceita qualquer tipo de E-mail, inválido ou não.

#### didYouMean
| Array | Propriedade | Descrição |
|--|--|--|
| didYouMean  | | |
|  `{}` | `array` didYouMean | x

#### emailVerification
| Array | Array | Propriedade | Descrição |
|--|--|--|--|
| emailVerification | | | |
|  `{}` | `syntaxVerification` 	| `boolean` isSyntaxValid 			| x
|  `{}` | `dnsVerification` 	| `boolean` isDomainHasDnsRecord 	| x
|  `{}` | `dnsVerification` 	| `boolean` isDomainHasWebRecord 	| x
|  `{}` | `dnsVerification` 	| `boolean` isDomainHasMxRecords 	| x
|  `{}` | `dnsVerification` 	| `array` recordDns 				| x
|  `{}` | `dnsVerification` 	| `array` recordWeb 				| x
|  `{}` | `dnsVerification` 	| `array` recordMx 					| x
|  `{}` | `mailboxVerification` | `array` 							| x

#### infrastructure
| Array | Array | Propriedade | Descrição |
|--|--|--|--|
| infrastructure  | | | |
|  `{}` | `mail` | `string` isSyntaxValid | x

#### sendAssess
| Array | Propriedade | Descrição |
|--|--|--|
| sendAssess  | | |
|  `{}` | `int` inboxQualityScore 		| x
|  `{}` | `string` sendRecommendation 	| x
|  `{}` | `string` sendStatus 			| x

#### spamAssess
| Array | Propriedade | Descrição |
|--|--|--|
| spamAssess  | | |
|  `{}` | `array` | x

#### social
| Array | Propriedade | Descrição |
|--|--|--|
| social  | | |
|  `{}` | `array` | x


### Json
```
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

Exemplos de Uso
------------
Para utilizar a chamada de API é preciso apenas efetuar uma requisição `https`. Toda linguagem de programação que permite uma requisição `https` pode ser utilizada.
Todos os exemplos utilizarão a `variável` `@endpoint`, para uso, é preciso alterar esta variável por sua requisição final, tendo atenção na na regra básica para os parâmetros necessários que são `email` e  `iPORTO_Api_ChavePublica`

```
@endpoint = 
https://api-v2.iporto.com.br/api-v2
/get
/email/xx@domain.com
/iPORTO_Api_ChavePublica/xx
```

### Curl
```
curl @endpoint
```

### Php
```
<?php
$get_json = file_get_contents(@endpoint);
```

### Javascript com jQuery
```
<script type="text/javascript">
$.getJSON(@endpoint, function(data) {
  get_json = data;
});
```

### Ruby
```
require "open-uri"
get_json = open(@endpoint).read
```

### Asp Clássico
```
<%
Set xmlHttp = Server.Createobject("MSXML2.ServerXMLHTTP.6.0") 
xmlHttp.Open "GET", @endpoint, False 
xmlHttp.Send 
_RESTfulResponse = xmlHttp.responseText 
xmlHttp.abort() 
set xmlHttp = Nothing 
get_json = _RESTfulResponse 
```

