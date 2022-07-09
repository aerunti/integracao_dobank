# Integração API de pagamento Dobank

Bem vindo à integração mais fácil e prática do mercado!

A integração com a API da Dobank foi desenvolvida para ser o mais simples possível. 

Usamos apenas enpoints POST. 
A autenticação é feita com o envio  do token como variável post. 

1. Acesse sua conta no Dobank, vá em Configurações -> Api de pagamento
2. Defina as taxas adicionais, se desejar, para pix e BTC
3. Informe a URL do seu webhook para receber as informações de retorno
4. Copie o token já gerado. Você pode trocar se desejar. 
5. implemente  a integração seguindo os modelos abaixo:

## Pagamento (em python/requests) - exemplos em outras linguagens podem ser adicionadas posteriormente, a pedido

    import json
    import requests
    url = 'https://dobank.capital/api/'
    endpoint = 'pagamento'

    token = '<SEUTOKEN>'
    valor = 1.00 # R$ 1,00
    metodo = 'pix' # ou 'btc' para bitcoin

    payload = {
        "token": token,
        "amount": valor,
        "method_code":metodo,#or "btc"
    }
    #print(str(user))
    r = requests.post(url+endpoint, data=payload)

    #print(r.url, r.content, r.status_code)
    a = r.json()
    print(a)
    #adicione o seu código para registrar as informações no banco de dados



## Exemplo de retorno (JSON)

    {
    "txid": "c7652832d678df00100a55bf87df7e87",
    "copiaecola": "00020101021226910014br.gov.bcb.pix2569api.developer.btgpactual.com\/v1\/p\/v2\/ef6a95c8168b4aec8fc36201d1421e795204000053039865802BR5925Dobank Tecnologia em Paga6011So Paulo SP62070503***6304E8D4",
    "qrcode": "iVBORw0KGgoAAAANSUhEUgAAAPQAAAD0CAYAAACsLwv+AAAAAklEQVR4AewaftIAAA4\/SURBVO3BQY4cy5LAQDLR978yR0tfBZCoaun9GDezP1hrXeFhrXWNh7XWNR7WWtd4WGtd42GtdY2HtdY1HtZa13hYa13jYa11jYe11jUe1lrXeFhrXeNhrXWNh7XWNR7WWtf44UMqf1PFicpUMal8U8WkMlWcqEwVb6hMFW+oTBUnKr+pYlI5qThRmSreUPmbKj7xsNa6xsNa6xoPa61r\/PBlFd+k8psqTlROVKaKNyomlaliUjlRmSomlaliUpkqTipOVKaKSeWkYlL5hMpU8UbFN6l808Na6xoPa61rPKy1rvHDL1N5o+INlaliUnlDZar4hMpUMamcqEwVk8pUcVIxqUwV31RxUvEJlaliqphUvknljYrf9LDWusbDWusaD2uta\/xwuYpPqJxUTCpTxScq3lCZKiaVN1SmijdUpopJ5RMVk8pJxaQyVfwve1hrXeNhrXWNh7XWNX64nMpvUpkqTlROKiaVqeINlb9J5RMVk8pUMal8ouImD2utazysta7xsNa6xg+\/rOJfqphU3qiYVKaKSWWqmCpOVKaKSeWk4g2Vk4pJ5aRiUnlD5URlqjhR+U0V\/yUPa61rPKy1rvGw1rrGD1+m8l+iMlVMKlPFpDJVTCpTxaQyVUwqU8WkMlVMKicqU8UbKlPFpPJNFZPKVDGpTBVvqEwVJyr\/ZQ9rrWs8rLWu8bDWuob9wf8wlTcqTlROKiaV31QxqZxUvKEyVXxC5Y2KE5Wp4g2Vk4qbPKy1rvGw1rrGw1rrGvYHH1CZKiaVb6p4Q2WqmFROKr5J5RMVk8pvqphU3qiYVE4qJpU3Kr5J5ZsqftPDWusaD2utazysta7xw5epTBVvqEwVn6iYVE4qPqEyVZxUfFPFicpUMalMKlPFpHKiclLxRsUbKlPFicpUMam8UTGpTBXf9LDWusbDWusaD2uta\/zwZRWTylRxUjGpTBUnKm9UTCpTxYnKVHFScaLyRsU3VZyonFS8ofKGyknFVDGpnFR8omJS+Zse1lrXeFhrXeNhrXWNHz5UcVIxqZxUTBX\/n1S8oTJVTCqfUJkqJpVJ5RMVk8pUMamcqEwVJypvVJxUTCq\/6WGtdY2HtdY1HtZa1\/jhl6lMFW+oTBVvVHxCZar4hMobFW+ofELljYoTlaliUplUTlSmikllqphUTipOVCaV\/5KHtdY1HtZa13hYa13D\/uCLVN6oeEPlmyomlaliUpkqJpWTik+oTBWTylTxCZVPVHyTyknFGyonFZPKVDGpvFHxTQ9rrWs8rLWu8bDWusYPX1bxhspUMan8l1RMKlPFpPKGyjepnFRMKicVb6hMFZPKScUbKlPFGxUnFZPKVHGiMqlMFZ94WGtd42GtdY2HtdY1fviQym+qmFTeqDhRmSr+pYo3VKaKSWWqOKn4hMpUMalMFScqU8WkMlVMKlPFVDGpTBUnFf8lD2utazysta7xsNa6hv3BB1Smim9SmSreUJkqJpU3Kt5Q+U0Vk8pvqphU3qg4UXmjYlL5RMUnVKaKSWWq+KaHtdY1HtZa13hYa13D\/uB\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\/k8pU8U0Pa61rPKy1rvGw1rqG\/cE\/pHJScaJyUjGpfKLiDZWpYlKZKt5Q+aaKE5U3KiaVqeINlaliUjmpOFF5o+JEZaqYVKaKTzysta7xsNa6xsNa6xo\/fEjlpGJSeUNlqpgqJpVJ5aTiDZWTik+ofKJiUpkqTlSmiqliUpkqJpUTlanipOKbVE4qJpUTlROV3\/Sw1rrGw1rrGg9rrWv88KGKSWVSmSo+oTJVTBUnKm+onFS8oTJVnKhMFZ9QmSreUHmj4kTlROWkYqp4o+JEZao4qZhU\/qaHtdY1HtZa13hYa13jhy+rOFGZKk5U\/iaVb6qYVCaVqWKqOFH5hMqJylTxhsobKp9QmSomlU+onFT8Sw9rrWs8rLWu8bDWusYPf1nFGxUnKm9UTConFZPKicpU8QmVNyreUJkqPqFyUjGpTBXfpPJGxRsqk8pUcaLyTQ9rrWs8rLWu8bDWusYPH1L5myqmihOVSWWqmFROKiaVT1S8UTGpnKhMFScqJxWTylQxqUwqJypTxaRyUjGpTBWTyonKVHFScaIyVXzTw1rrGg9rrWs8rLWu8cOXVXyTyonKVPGGyonKGxUnFZPKb6p4o2JSeUPljYpJ5aRiUvlNFd9UMalMFZ94WGtd42GtdY2HtdY1fvhlKm9U\/KaKN1T+popJ5Q2Vb6p4o+JEZVKZKiaVk4pJ5RMqv0nlNz2sta7xsNa6xsNa6xo\/XEZlqnhD5Y2KSWWqeENlqphUTireUHlDZaqYVKaKk4qTihOVqWJSmVTeqJhU3lA5qfimh7XWNR7WWtd4WGtd44fLVJyoTBVTxaQyVUwqb6i8oTJVTCqTylQxqbyhMlVMKlPFScWkclIxqUwVk8pUcaIyVUwqU8WkclIxqfymh7XWNR7WWtd4WGtd44dfVvGbKiaVk4oTlanimyo+oTJVnKhMFd9UMal8omJSmSomlaliUjmpOKmYVKaKNyp+08Na6xoPa61rPKy1rvHDl6n8TSpTxaQyqUwVb6i8oTJVTCpvVJyoTBWTylQxqXyiYlKZKiaVk4pJ5W9SmSpOVN6o+KaHtdY1HtZa13hYa13D\/mCtdYWHtdY1HtZa13hYa13jYa11jYe11jUe1lrXeFhrXeNhrXWNh7XWNR7WWtd4WGtd42GtdY2HtdY1HtZa13hYa13j\/wBxKAtPnvYhdwAAAABJRU5ErkJggg=="
}


Atenção:

**txid** é o número da transação que você deve registrar no seu banco de dados para vincular esse pagamento

**copiaecola** é o código copia e cola para você retornar ao seu cliente na sua interface

**qrcode** é a imagem qrcode em base64 para você exibir ao seu cliente

## html
Segue um exemplo de como mostrar o codigo qr e o copiaecola em html

    <!DOCTYPE html>

    <div>
    <img src="data:image/png;base64,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">
    <br>
    <button class="btn btn-success" onclick="copyPix();">Copiar Código PIX </button>



    </div>
    <script>
    function copyPix() {

    /* Copy the text inside the text field */
    navigator.clipboard.writeText('00020101021226910014br.gov.bcb.pix2569api.developer.btgpactual.com/v1/p/v2/3694771894b9437fbfcee755d981b02f5204000053039865802BR5925Dobank Tecnologia em Paga6011So Paulo SP62070503***63048847');

    /* Alert the copied text */
    /*   alert("Pix copiado: 00020101021226910014br.gov.bcb.pix2569api.developer.btgpactual.com/v1/p/v2/3694771894b9437fbfcee755d981b02f5204000053039865802BR5925Dobank Tecnologia em Paga6011So Paulo SP62070503***63048847" ); */
    }
    </script>

    </html>

6. Aguarde seu cliente efetuar o pagamento. 

7. Retorno do pagamento. 

Você pode consultar os pagamentos dos últimos 2 dias:

    

    import json
    import requests
    url = 'https://dev.dobank.capital/api/'
    endpoint = 'pagamentos'

    token = '<SEUTOKEN>'



    payload = {
        "token": token
    }
    #print(str(user))
    url = url+endpoint
    print(url, payload)
    r = requests.post(url, data=payload)

    # print(r.url, r.content, r.status_code)
    a = r.json()
    print(a)
    #adicione o seu código para registrar as informações no banco de dados

Exemplo de retorno:

    [
        {
            "trxid": "VNJ9BHNC4NW6",
            "method_code": "pix",
            "amount": "1.00000000",
            "amount_charged": "1.51200000",
            "status": "Aguardando Pagamento"
        },
        {
            "trxid": "SR4SHNC9B8D9",
            "method_code": "pix",
            "amount": "2.00000000",
            "amount_charged": "2.52400000",
            "status": "Aguardando Pagamento"
        }
    ]


ou um pagamento específico 





exemplo de retorno de pagamento específico



    [
        {
            "trxid": "VNJ9BHNC4NW6",
            "method_code": "pix",
            "amount": "1.00000000",
            "amount_charged": "1.51200000",
            "status": "Aguardando Pagamento"
        }
    ]


Exemplo de retorno de erro:

    {
        "error": "N\u00e3o foram encontrados registros"
    }


8. Webhook

Alternativamente, ao invês de ficar consultado periodicamente para checar se o pagamento foi feito, você pode configurar um webook - um endpoint post na sua aplicação -  para ser notificado quando ocorrer o pagamento:

    https://meusite.com.br/webook_dobank



o webhook receberá uma mensagem no mesmo formato da consulta individual:

        [
            {
                "trxid": "VNJ9BHNC4NW6",
                "method_code": "pix",
                "amount": "1.00000000",
                "amount_charged": "1.51200000",
                "status": "Pago"
            }
        ]

é recomendado que se configure o webhook para só receber mensagens de https://dobank.capital

