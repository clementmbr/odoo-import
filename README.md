---
description: Tutorial realizado pela Akretion - www.akretion.com.br
---

# Funcionamento da importação

Para importar dados no [Odoo](http://odoo.com), basta clicar no botão _Import_ da página do tipo de objeto desejado e selecionar o arquivo Excel com os dados do objeto a ser importado.

![](.gitbook/assets/image%20%2817%29.png)

Para saber como preencher esse arquivo Excel \(nome e conteúdo das colunas\), um método básico é de **primeiro exportar** um arquivo .xls de uma lista de objetos existentes com a opção '_Update data \(import-compatible export\)_' e a lista dos campos que você quer importar.

## Exportar dados

Para exportar dados do Odoo para arquivos Excel \(ou CSV\), é preciso fazer aparecer os objetos para ser exportados em visualização '**lista**'. Isso permite selecionar os objetos para serem exportados. Quando selecionar um objeto aparece o botão **Ação** que permite, entre outras coisas, exportar os dados dos objetos selecionados :

![](.gitbook/assets/image%20%282%29%20%282%29.png)

![](.gitbook/assets/image%20%281%29.png)

Uma vez que você tiver exportado esse arquivo .xls, você pode **realizar uma cópia com os mesmos títulos de colunas** e formatar os dados para serem importados da mesma maneira que os itens exportados.

Agora, a complexidade da importação de dados no Odoo vem da complexidade em registrar no Odoo **as relações** entre os objetos importados.

## Como importar relações entre objetos ?

Vamos tomar um exemplo. Um dos campos dos objetos do tipo _Contato_ é o campo _Marcadores_ \(chamado também de "Categoria de contato", ou "Tag do contato"\). Para associar cada contato importado com um Marcador específico temos que :

1.  Importar todos os _Marcadores_ **antes** de importar os _Contatos_.
2.  Na coluna dos _Marcadores_ do arquivo Excel de importação dos _Contatos_, indicar os _**External ID**_ dos _Marcadores_  de cada _Contato_ importado , para indicar qual _Marcador_  está associado a qual _Contato_.

O _External ID_, chamado também de _**XML ID**_, é o identificador de um objeto presente no Odoo. Ele permite fazer a diferença por exemplo entre dois _Marcadores_ que teriam o mesmo nome no Odoo apesar de serem dois objetos distintos do mesmo tipo _'Marcador'_.

{% hint style="info" %}
É importante anotar a [diferença entre o External ID de um de um objeto e o ID no banco de dados](https://www.odoo.com/documentation/user/12.0/general/base_import/import_faq.html#what-s-the-difference-between-database-id-and-external-id) desse mesmo objeto.

Os dois são identificadores únicos do mesmo objeto, porém o _ID_ no banco de dados é um **número** \(único\) dado automaticamente por Odoo quando cria \(ou importa\) esse novo objeto, enquanto o _External ID_ é uma **cadeia de caracteres** que pode ser dada pelo usuário durante a importação do objeto.
{% endhint %}

É possível conhecer o _External ID_ de um objeto diretamente pela **interface** do Odoo ou quando **exporta** dados do Odoo para arquivos \(Excel ou CSV\).

## _External ID_ pela interface

Primeiro é preciso ativar o [modo "desenvolvedor" ](https://odoo-development.readthedocs.io/en/latest/odoo/usage/debug-mode.html)do Odoo no painel de Configurações gerais :

![](.gitbook/assets/image%20%284%29.png)

Depois ir na página do objeto desejado, por exemplo esse Marcador de contato \(chamado também de "Tag do contato", acessível pelo menu _Contatos_ &gt; _Configuração_ &gt; _Tags do contato_\), clicar na barata que apareceu \(encima na direita\), e abrir _Visualizar Metadata_ do objeto corrente :

![](.gitbook/assets/image.png)

Aparece então as suas Metadatas, incluindo o **ID XML** \(outro nome para o External ID\), diferente  do ID "simples" que é o identificador do objeto no banco de dados \(que não precisamos usar\) :

![](.gitbook/assets/image%20%289%29%20%281%29.png)

## External ID na exportação

Ao exportar _Marcadores_ de contato, para seguir o nosso exemplo, basta selecionar a opção '_Update data_' para fazer aparecer o campo '_ID Externo_' dentro dos campos disponíveis :

![](.gitbook/assets/image%20%2810%29%20%281%29.png)

O resultado é um arquivo Excel com a lista dos _External ID_ de cada _Marcador_ :

![](.gitbook/assets/image%20%286%29.png)

{% hint style="warning" %}
Apesar do título da coluna ser "id", é uma cadeia de caracteres, então é a coluna do nosso _**External ID**_. 
{% endhint %}

## Criação do _External ID_ durante a importação

Um bom hábito para facilitar o processo de importação é de você **escolher/escrever os próprios External ID dos objetos que você está importando**. Desta maneira quando precisar importar outros tipos de objetos relacionados com os primeiros, você já conhecerá os External ID de referencias deles.

Por exemplo, se eu importar alguns _Marcadores_ com o seguinte arquivo Excel :

![](.gitbook/assets/image%20%288%29%20%281%29.png)

Basta clicar no botão _Import_ &gt; _Carregar Arquivo_ da página '_Tags do Contato_' e selecionar o arquivo para importar. O Odoo reconhece o significação das colunas do meu arquivo mas é sempre possível escolher manualmente o destino de cada uma :

![](.gitbook/assets/image%20%283%29%20%281%29.png)

{% hint style="info" %}
Caso não estiver preenchida a coluna "_External ID_", o Odoo criará automaticamente e importará o objeto mesmo assim.
{% endhint %}

Podemos finalmente verificar pela interface que o _External ID_ de cada _Marcador_  importado corresponde a cadeia de caracteres indicada no arquivo de importação. Será então possível usar esse mesmo _External ID_ no futuro, por exemplo durante a importação dos Contatos para indicar o _Marcador_ de cada _Contato_ :

![](.gitbook/assets/image%20%2811%29%20%281%29.png)

## Relação pai / filho

Na mesma ideia que para importar a informação da relação entre dois objetos de tipos diferentes, o jeito mais simples e seguro de importar as relações entre dois objetos do mesmo tipo é de :

1. importar os pais
2. importar os filhos, indicando para cada filho o _External ID_ do\(s\) pai\(s\) previamente importados

Por exemplo, importando o arquivo :

![](.gitbook/assets/image%20%281%29%20%281%29.png)

Eu vou poder importar 2 _Marcadores_ como sub-categorias de contato da categoria pai "_Meu Marcador importado 1_" :

![](.gitbook/assets/image%20%287%29%20%281%29.png)

{% hint style="info" %}
Na teoria é possível importar junto no mesmo arquivo .xls ou .CSV os objetos filhos e os pais relacionados de uma vez. Porém é mais complexo e é fonte de erros, por isso recomendamos de realizar esse tipo de importações pai/filho em duas vezes.
{% endhint %}

{% hint style="info" %}
Alguns objetos Odoo podem ter **2 pais ou mais** \(o tipo de campo ligando um filho aos seus pais é então chamado de "_one2many_" ou "_many2many_"\), como os marcadores de Contato por exemplo.

Nesta situação é só indicar os 2 \(ou mais\) External ID, separados por [**uma vírgula, sem espaço**](https://www.google.com/url?q=https://www.odoo.com/documentation/user/12.0/general/base_import/import_faq.html%23how-can-i-import-a-many2many-relationship-field-e-g-a-customer-that-has-multiple-tags&sa=D&source=hangouts&ust=1587566898977000&usg=AFQjCNEHDhSJsqBye6JvcCEeoCsoU4G3zQ). Exemplo :

_marcador\_de\_contato\_1,marcardor\_de\_contato2_
{% endhint %}

{% hint style="warning" %}
Se um filho para importar não tem pai, **deixar a célula vazia**. Se escrever "0" ou False vai retornar um erro de importação.
{% endhint %}

## FAQ oficial da Odoo S.A.

Para questões técnicas específicas sobre a importação :

{% embed url="https://www.odoo.com/documentation/user/12.0/general/base\_import/import\_faq.html" %}











