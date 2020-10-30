- Estrutura de pastas e arquivos
- Caminhos da parte técnica
- Fazer a poc com o projeto exemplo
- Como refatorar cockpit?

* Primeiro milestone: Faz sentido?
- O que fazer para que o cockpit vire um monorepo?


Reestruturação do projeto
- Back e front projetos separados (Containers separados)
. Front seria servido por um container nginx

* Como gerenciar a sessão do usuário escalando os front ends?
- Usuário deve poder se logar pelo accounts
- Usuário deve poder se logar pelo cognito


- Front:
* Necessário utilizar o jwt
. Sales -> oms.chaordic.com.br/sales/some_path_of_sales
. Finance -> oms.chaordic.com.br/finance/some_path_of_sales
. Logistics -> oms.chaordic.com.br/logistics/some_path_of_sales

-> Sacaria o express session da jogada e passaria a utilizar o jwt

- payload do jwt
```json
{
  "id": "xxxxxxxxxx",
  "email": "johndoe@linx3.com",
  "organization": ["qa", "qab2cerp", "linxdemostorex"],
  "scopes": [
    "br.com.chaordic.cockpit/sales/customerServices/stockout",
    "br.com.chaordic.cockpit/sales/",
    "br.com.chaordic.cockpit/sales/customerServices/stockout",
    "br.com.chaordic.cockpit/sales/customerServices/pickupFail/*",
    "br.com.chaordic.cockpit/sales/customerServices/deliveryLost/cancel"
    "br.com.chaordic.cockpit/sales/customerServices/changeStatus",
    "br.com.chaordic.cockpit/logistics/locations/*",
    "br.com.chaordic.cockpit/logistics/stocks/*",
    "br.com.chaordic.cockpit/finance/reports",
    "br.com.chaordic.cockpit/finance/config"
  ],
  "iat": 1604004921,
  "kind": "acc",
  "exp": 1619556921,
  "aud": "users",
  "iss": "linx-accounts",
  "sub": "xxxxxxxxxx"
}
```
- No accounts
* br.com.chaordic.cockpit -> Application

Groups
------
group 1
scopes: ["br.com.chaordic.cockpit/sales/customerServices/*"]

group 2
scopes: ["br.com.chaordic.cockpit/inventory/locations*"]

User
----
user1 
groups: ["group1", "group2"]

scopes
scopes: ["br.com.chardic.cockpit/sales/customerServices/*", "br.com.chaordic.cockpit/inventory/locations/*"]

put('/groups', {name: group1, scopes: [ 'br.com.chaordic.cockipt/sales/customerServices/*' ]})
post('/groups', {name: group1, scopes: [ 'br.com.chaordic.cockipt/sales/customerServices/*' ]})
patch('/groups', {name: group1, scopes: [ 'br.com.chaordic.cockpit/sales/customerServices/*' ]})
delete('/groups', {name: group1, scopes: [ 'br.com.chaordic.cockpit/sales/customerServices/*' ]})
