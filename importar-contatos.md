# Importar contatos

O video oficial da Odoo S.A. é um bom primeiro passo caso estiver descobrindo a organização dos _Contatos_ no Odoo :

{% embed url="https://youtu.be/BDcVuozHrOg" %}

O único campo obrigatório para a criação de um Contato é o _Nome_, por isso é teoricamente possível importar um arquivo com apenas uma lista de nomes e criar facilmente centenas de Contatos.

Porém, um _Contato_ em Odoo pode apontar para vários outros objetos Odoo. Por isso, como a gente indicou na introdução, é necessário [importar primeiramente todos esses objetos antes de finalmente importar os Contatos](./#como-importar-relacoes-entre-objetos) indicando o External ID de cada objeto com qual cada Contato estará relacionado.

## Importações anteriores aos Contatos

O método básico para importar qualquer objeto em Odoo é de **primeiro exportar** um arquivo .xls de uma lista de objetos com a opção '_Update data \(import-compatible export\)_' e a lista dos campos que você quer importar :

![](.gitbook/assets/image%20%281%29.png)

Uma vez que você tiver exportado esse arquivo .xls, você pode preencher esse mesmo arquivo com os dados para ser importados, usando os mesmos títulos das colunas.

Segue a lista exaustiva dos objetos Odoo a ser importados antes da importação de Contatos, indicando cada vez a onde encontrar esse objeto na interface de Odoo.

### Bancos

![](.gitbook/assets/image%20%282%29.png)

### Contas Bancárias

![](.gitbook/assets/image%20%285%29.png)

### Condições de Pagamento

![](.gitbook/assets/image%20%2818%29.png)

### Posições Fiscais

![](.gitbook/assets/image%20%283%29.png)

### Lista de preços

![](.gitbook/assets/image%20%289%29.png)

### Marcadores de Contato \(ou "Tags do Contato", ou "categoria de Contato"\)

Seguindo as etapas que a gente viu [na introdução](./#criacao-do-external-id-durante-a-importacao).

### Tratamento para o contato

![](.gitbook/assets/image%20%288%29.png)

## Importação dos contatos

[Como explicamos na introdução](./#relacao-pai-filho), é importante realizar em primeiro a importação dos Contatos "pai" \(como uma empresa\) e depois os Contatos "filho" \(como os membros de uma empresa\) ligados aos Contatos "pai" pelo External ID desses.

Segue uma lista dos campos interessantes para uma importação de Contatos com todas as relações possíveis :

| Título coluna | Conteúdo |
| :--- | :--- |
| **id** |  |
| **name** |  |
| **title/id** |  |
| **is\_company** |  |
| **customer** |  |
| **supplier** |  |
| **active** |  |
| **type** |  |
| **parent\_id/id** |  |
| **country\_id** |  |
| **lang** |  |
| **category\_id/id** |  |
| **property\_product\_pricelist/id** |  |
| **property\_account\_position\_id/id** |  |
| **property\_account\_receivable\_id/id** |  |
| **property\_account\_payable\_id/id** |  |
| **property\_payment\_term\_id/id** |  |
| **property\_supplier\_payment\_term\_id/id** |  |
| **customer\_payment\_mode\_id/id** |  |
| **supplier\_payment\_mode\_id/id** |  |
| compte bancaire |  |

 

