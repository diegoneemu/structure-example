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
