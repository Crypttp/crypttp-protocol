# crypttp-protocol
Cryptocurrencies and virtual currencies transfer protocol

## Abstract

This protocol proposes a URI scheme for making cryptocurrencies and virtual currencies payments.
It was designed to improve and expand the capabilities of [BIP21](https://github.com/bitcoin/bips/edit/master/bip-0021.mediawiki) 

## Motivation
1. Enable users to easily make payments by simply clicking links on webpages or scanning QR Codes or clicking buttons at webpages and mobile apps.
2. Give users the ability to choose which cryptocurrency wallet application to use to complete the transaction.
3. Combine all cryptocurrencies into one URL scheme, as any cryptocurrency is a currency.
4. Change the acquiring solutions so that they only accept cryptocurrency for the seller without any interface, since the user can choose the currency to pay for the order in the multicurrency wallet or at the time of choosing a wallet.

## Specification
```
scheme="crypttp"
host="crypttp.com"
pathPrefix="/crypttp"
example="crypttp://crypttp.com/crypttp"
```

## Query Keys

The params passed over protocol in base64 format.
```
crypttp://crypttp.com/crypttp?params=eyJpZCI6Im1lcmNoYW50X2lkIiwicGFyYW1zIjpbWyJFVEgiLCIxLjY0NDY5MTE4NjY3NTkxOTUiLCIweGQzODZkMDQ1ZThkZDkzOEYwRGI3NTYyMjhlQWUzQzY0QUMwNWNBYjUiLCJtZXNzYWdlKHBheWxvYWQvZGF0YSkiLCJtZW1vIiwic3VjY2Vzc191cmwiLCJlcnJvcl91cmwiXSxbIlhMTSIsIjQ1NTcuNjkyMzA3NjkyMzA4IiwiR0RHVVVNUjNGS0VCVUc0NVJaVFJRQkJQQjJBSlZZWUZVQ0VaWkZJNUpQVjIyRVpKNFNSREtLTkMiLCJtZXNzYWdlKHBheWxvYWQvZGF0YSkiLCJtZW1vIiwic3VjY2Vzc191cmwiLCJlcnJvcl91cmwiXV19
```

#### parsed params
```JSON
{
  "id":"merchant_id",
  "params":[
    [
      "ETH",
      "1.6446911866759195",
      "0xd386d045e8dd938F0Db756228eAe3C64AC05cAb5",
      "message(payload/data)",
      "memo",
      "success_url",
      "error_url"
    ],
    [
      "XLM",
      "4557.692307692308",
      "GDGUUMR3FKEBUG45RZTRQBBPB2AJVYYFUCEZZFI5JPV22EZJ4SRDKKNC",
      "message(payload/data)",
      "memo",
      "success_url",
      "error_url"
    ]
  ]
}
```

#### params specification

* `id` `{STRING}` - merchant id that is required to track which merchant initiated transaction
* `params` `{ARRAY}` - array of arrays containing transaction details for each payment type (currency)
* `params[0][0]` `{STRING}` - ticker of currency which user want to pay with
* `params[0][1]` `{STRING}` - amount of `params[0][0]`. That amount **not include** network fee, so it should be **adjusted**. It is the exact amount that merchant is waiting to receive. 
Correct regex pattern for amount is: `/^\d+\.\d+$/`
* `params[0][2]` `{STRING}` - address that varies depending on the blockchain
* `params[0][3]` `{STRING}` - message / data / payload that should be appended to transaction
* `params[0][4]` `{STRING}` - special id which is used to identify the recipient in a transaction in some blockchains
* `params[0][5]` `{STRING}` - url where user should be redirected back if transaction succeed
* `params[0][6]` `{STRING}` - url where user should be redirected back if transaction failed

# Integration

[React JS](https://github.com/Crypttp/crypttp-react)

[Vue JS](https://github.com/Crypttp/crypttp-vue) 

[Angular JS](https://github.com/Crypttp/crypttp-angular) 

[Swift](https://github.com/Crypttp/crypttp-ios-sdk) 

[Java/Kotlin](https://github.com/Crypttp/crypttp-android-sdk) 
