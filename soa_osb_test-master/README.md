# Teste back-end developer


O teste é simples porém prático, pois você verá muito disso caso você venha a participar do nosso ambiente de trabalho.

# Descrição do Teste

Vamos supor que necessitamos realizar uma conexão com um novo broker de hotéis, que é um parceiro de negócio e possui um webservice onde expõe a sua API.

Porém não gostaríamos que nosso front-end bata diretamente nesse broker, por questões de segurança.

Sendo assim precisamos que você construa uma API para intermediar o acesso entre nosso front-end e o broker.

### API do nosso parceiro:

Nosso parceiro irá disponibilizar uma API de consulta de hotéis por cidade:

**Descrição da API**

**URL: https://cvcbackendhotel.herokuapp.com/hotels/avail/{ID_da_Cidade}**

**Method: GET**

***A API responde os seguintes ID_da_Cidade:***

1. ***1032*** (Porto Seguro)
2. ***7110*** (Rio de Janeiro)
3. ***9626*** (São Paulo)

***Exemplo:***
> **URL: https://cvcbackendhotel.herokuapp.com/hotels/avail/1032**

```json
// Response
[{
  "id": 1,
  "name": "Hotel Teste 1",
  "cityCode": 1032,
  "cityName": "Porto Seguro",
  "rooms": [
    {
      "roomID": 0,
      "categoryName": "Standard",
      "price": {
        "adult": 1372.54,
        "child": 848.61
      }
    }
  ]
}]
```

Ele também irá disponibilizar uma API para buscar os detalhes do Hotel pelo seu código:

**URL: https://cvcbackendhotel.herokuapp.com/hotels/{ID_Do_Hotel}**

**Method: GET**

***Exemplo:***
> **URL: https://cvcbackendhotel.herokuapp.com/hotels/1**


```json
// Response
[{
  "id": 1,
  "name": "Hotel Teste 1",
  "cityCode": 1032,
  "cityName": "Porto Seguro",
  "rooms": [
    {
      "roomID": 0,
      "categoryName": "Standard",
      "price": {
        "adult": 1372.54,
        "child": 848.61
      }
    }
  ]
}]
```
# Teste 1:

Nosso front-end não faz nenhuma regra de negócio, sendo assim precisamos que o serviço já traga o valor da viagem do passageiro para ser exibida.

1. Construa uma API Rest com a arquitetura que achar melhor:
2. O serviço do broker retorna apenas o valor por dia sendo assim precisamos calcular o valor total da viagem e adicionar a comissão para cada um dos quartos retornados

**Detalhes de como calcular o valor total da viagem**

A API do broker só retorna o valor da diária sendo assim precisamos pegar esse valor e calcular os dias que o cliente gostaria de ficar ex:

**Checkin dia: 20/05/2017, Checkout dia: 25/05/2017, Total de Adultos: 2 com 1 Criança**

***Considerando as datas acima o cliente gostaria de ficar 5 dias no hotel, sendo assim calculamos o valor total da viagem da seguinte forma:***

Vamos supor que o valor retornado pela API do broker foi R$ 100,00 para adulto e R$ 50,00 para criança:
  1. Pegar a quantidade de dias e multiplicar pelo valor do Adulto
  2. Pegar a quantidade de dias e multiplicar pelo valor do Criança
  3. Adicionar a comissão de .70 para adulto e para criança
    * Formula para fazer isso ***({valorViagemAdulto}/0.7)*** Ex: (500/0.7);
  4. Somar tudo e você terá o ***totalPrice***

### Detalhes do serviço
**URL: Construa a URL como achar melhor**
**Method: GET**

***Parametros obrigatórios:***
1. CityCode
2. Checkin
3. Checkout
4. Quantidade de Adultos
5. Quantidade de Crianças

**Resposta do Serviço**

Obs.: Todos os valores retornados por esse serviço são adicionados o valor de comissão.

```json
{
  "id": 1,
  "cityName": "Porto Seguro",
  "rooms":[{
      "roomID": 1,
      "categoryName": "Standard",
      "totalPrice": 10000.00,
      "priceDetail": {
        "pricePerDayAdult": 500.00,
        "pricePerDayChild": 50.00
      }
    }]
}
```


# Teste 2:

Construir um serviço que retorne os detalhes do hotel utilizando a mesma regra acima porem passando o id do hotel que gostaria de consulta.

Utilizar o serviço ***"Detalhes do Hotel por código de hotel"*** descrito na explicação acima.

**URL: Construa a URL como achar melhor**
**Method: GET**

***Parametros obrigatórios:***
1. HotelID

O Hotel ID é o ID do serviço retornado na url:
> **https://cvcbackendhotel.herokuapp.com/hotels/avail/1032**

**Resposta do Serviço**

```json
{
  "id": 1,
  "cityName": "Porto Seguro",
  "rooms":[{
      "roomID": 1,
      "categoryName": "Standard",
      "totalPrice": 10000.00,
      "priceDetail": {
        "pricePerDayAdult": 500.00,
        "pricePerDayChild": 50.00
      }
    }]
}
```


# Observações

Estamos falando de uma aplicação de alta disponibilidade, com isso presamos muito a ***VELOCIDADE*** e qualquer segundo é importante, sendo assim te damos alguns conselhos:
>1. Construa uma API com o máximo de performance possível
>2. Tente executar algum dos processos em paralelo assim você pode ganhar tempo na resposta. ;-)

Construa os dois serviço e faça o deploy em um repositório GitHub ou nos envie por e-mail.

Qualquer dúvida nos avise.

# Muito Boa Sorte e estamos ansiosos para receber seu código.
