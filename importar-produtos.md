---
description: ...com o módulo `l10n_br_fiscal` da Akretion instalado
---

# Importar produtos

O módulo [l10n\_br\_fiscal](https://github.com/akretion/l10n-brazil/tree/12.0-mig-l10n_br_account_product/l10n_br_fiscal) desenvolvido pela [Akretion](https://akretion.com/pt-BR) permite ter no Odoo **a integralidade dos categorias fiscais necessárias** ao cadastramento oficial de qualquer tipo de produto, incluindo o NCM, NBS, NBM, CEST e outros :

![](.gitbook/assets/image%20%2811%29.png)

Como qualquer outro objeto Odoo, o processo para importar produtos é de [primeiro **exportar** alguns produtos](importar-contatos.md#importacoes-anteriores-aos-contatos) atuais com a lista dos campos que você deseja importar, com a opção "_Update data \(import-compatible export\)_" e o formato Excel.

![](.gitbook/assets/image%20%2832%29.png)

## Campos para importar

É possível importar a lista de campos que você precisar, porém alguns campos são obrigatórios e devem ser importados como :

* o Nome
* o Tipo
* a Categoria
* o Tipo Fiscal
* a origem do ICMS
* o NCM
* e o Gênero Fiscal

Nessa ideia, uma lista  mínima de campos para exportar e preparar o seu arquivo Excel para importação seria essa :

![](.gitbook/assets/image%20%2826%29.png)

Cuidando de [importar os _External ID_ dos objetos que jà existem](./#como-importar-relacoes-entre-objetos) no Odoo para realizar a conexão com o seu novo produto importado.

<table>
  <thead>
    <tr>
      <th style="text-align:left">T&#xED;tulo da coluna do arquivo .xls</th>
      <th style="text-align:left">Conte&#xFA;do</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><b>id</b>
      </td>
      <td style="text-align:left">
        <p><em>External ID</em> dado ao <em>Produto</em> importado.</p>
        <p>Se deixar vazio o Odoo criar&#xE1; um automaticamente.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>name</b>
      </td>
      <td style="text-align:left">Nome do seu <em>Produto</em> no Odoo.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>type</b>
      </td>
      <td style="text-align:left">
        <p>Tipo de <em>Produto.</em> Escolher entre :</p>
        <ul>
          <li>&quot;<b>Produto</b>&quot; : para os produtos armazen&#xE1;veis que ser&#xE3;o
            seguidos no aplicativo de Invent&#xE1;rio.</li>
          <li>&quot;<b>Consum&#xED;vel</b>&quot; : para os produtos f&#xED;sicos cuja
            quantidade n&#xE3;o ser&#xE1; seguida no aplicativo de Invent&#xE1;rio.</li>
          <li>&quot;<b>Servi&#xE7;o</b>&quot; : para os servi&#xE7;os</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>categ_id/id</b>
      </td>
      <td style="text-align:left"><em>External ID </em>da <a href="importar-produtos.md#categoria-de-produto"><em>Categoria de Produto</em></a>,
        um tipo de objeto Odoo qui permite tratar juntos os <em>Produtos</em> da
        mesma categoria (como para necessidades cont&#xE1;veis por exemplo)</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>fiscal_type</b>
      </td>
      <td style="text-align:left">Um n&#xFA;mero entre 00 e 10 determinando o <a href="importar-produtos.md#tipo-fiscal">Tipo Fiscal</a> do
        produto.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>icms_origin</b>
      </td>
      <td style="text-align:left">Um n&#xFA;mero entre 0 e 8 determinando a <a href="importar-produtos.md#origem-do-icms">Origem do ICMS</a> do
        produto.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>ncm_id/id</b>
      </td>
      <td style="text-align:left">
        <p><em>External ID </em>do c&#xF3;digo NCM do Produto. <b>A integralidade dos 10770 c&#xF3;digos de NCM poss&#xED;veis j&#xE1; est&#xE3;o registrados</b> no
          Odoo com todas as suas caracter&#xED;sticas gra&#xE7;a ao m&#xF3;dulo l10n_br_fiscal
          da Akretion.
          <br />&#xC9; poss&#xED;vel encontr&#xE1;-los no menu <em>Fiscal &gt; Configura&#xE7;&#xE3;o &gt; NCM</em>.</p>
        <p></p>
        <p>Um <em>External ID </em>de um NCM ser&#xE1; sempre composto de &quot;l10n_br_fiscal.ncm_
          &quot; e seguido dos 8 n&#xFA;meros do c&#xF3;digo. Por exemplo :</p>
        <p>&quot;<b>l10n_br_fiscal.ncm_00000000</b>&quot;</p>
        <p>Para o <em>External ID </em>do NCM dos produtos &quot;sem NCM&quot;.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>fiscal_genre_id/id</b>
      </td>
      <td style="text-align:left">
        <p><em>External ID </em>do G&#xEA;nero Fiscal do Produto. Ele se encontra
          no menu <em>Fiscal &gt; Configura&#xE7;&#xE3;o &gt; G&#xEA;nero de Produto</em>.</p>
        <p></p>
        <p>Da mesma maneira que o <em>External ID </em>do NCM, ele &#xE9; do tipo<b> &quot;l10n_br_fiscal.product_genre_94&quot;</b>,
          os 2 &#xFA;ltimos n&#xFA;meros sendo o c&#xF3;digo do G&#xEA;nero do produto
          escolhido.</p>
      </td>
    </tr>
  </tbody>
</table>## Categoria de Produto

É preciso primeiro definir essas Categorias e depois exportá-las com o seu External ID. Elas se encontram no menu _Fiscal &gt; Produtos e Serviços &gt; Categorias de Produtos_ :

![](.gitbook/assets/image%20%2823%29.png)

Ou no menu _Inventário &gt; Configurações &gt; Categorias de Produtos_.

## Tipo Fiscal

Escolher o número seguindo o Tipo Fiscal desejado :

| Número | Tipo Fiscal |
| :--- | :--- |
| 00 | Mercadoria para Revenda |
| 01 | Matéria-prima |
| 02 | Embalagem |
| 03 | Produto em Processo |
| 04 | Produto Acabado |
| 05 | Subproduto |
| 06 | Produto Intermediário |
| 07 | Material de Uso e Consumo |
| 08 | Ativo Imobilizado |
| 09 | Serviços |
| 10 | Outros insumos |
| 99 | Outras |

{% hint style="info" %}
Esses _Tipos Fiscais_ são constantes no Odoo, **não é possível modificá-los**.
{% endhint %}

## Origem do ICMS

Escolher o número seguindo o Origem do ICMS desejado :

| Número | Origem do ICMS |
| :--- | :--- |
| 0 | 0 - Nacional, exceto as indicadas nos códigos 3, 4, 5 e 8  |
| 1 | 1 - Estrangeira – importação direta, exceto a indicada no código 6  |
| 2 | 2 – Estrangeira – adquirida no mercado interno, exceto a indicada no código 7 |
| 3 | 3 – Nacional – mercadoria ou bem com Conteúdo de Importação superior a 40% \(quarenta por cento\) e inferior ou igual a 70% \(setenta por cento\) |
| 4 | 4 – Nacional – cuja produção tenha sido feita em conformidade com os processos produtivos básicos de que tratam o Decreto-lei n° 288/67 e as Leis \(federais\) nos 8.428/91, 8.397/91, 10.176/2001 e 11.484/2007 |
| 5 | 5 – Nacional – mercadoria ou bem com Conteúdo de Importação inferior ou igual a 40% \(quarenta por cento\) |
| 6 | 6 – Estrangeira – importação direta, sem similar nacional, constante em lista de Resolução CAMEX e gás natural |
| 7 | 7 – Estrangeira – adquirida no mercado interno, sem similar nacional, constante em lista de Resolução CAMEX e gás natural |
| 8 | 8 – Nacional – mercadoria ou bem com Conteúdo de Importação superior a 70% \(setenta por cento\). \(cf. Ajuste SINIEF 15/2013\) |

{% hint style="info" %}
essas _Origens de ICMS_ são constantes no Odoo, **não é possível modificá-las**.
{% endhint %}



