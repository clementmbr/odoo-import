---
description: ...com o módulo `l10n_br_fiscal` da Akretion instalado
---

# Importar produtos

O módulo [l10n\_br\_fiscal](https://github.com/akretion/l10n-brazil/tree/12.0-mig-l10n_br_account_product/l10n_br_fiscal) desenvolvido pela [Akretion](https://akretion.com/pt-BR) permite ter no Odoo **a integralidade dos categorias fiscais necessárias** ao cadastramento oficial de qualquer tipo de produto, incluindo o NCM, NBS, NBM, CEST e outros :

![](.gitbook/assets/image%20%2810%29.png)

Como qualquer outro objeto Odoo, o processo para importar produtos é de [primeiro **exportar** alguns produtos](importar-contatos.md#importacoes-anteriores-aos-contatos) atuais com a lista dos campos que você deseja importar, com a opção "_Update data \(import-compatible export\)_" e o formato Excel.

![](.gitbook/assets/image%20%2830%29.png)

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

![](.gitbook/assets/image%20%2824%29.png)

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
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>icms_origin</b>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>ncm_id/id</b>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>fiscal_genre_id/id</b>
      </td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>## Categoria de Produto

É preciso primeiro definir essas Categorias e depois exportá-las com o seu External ID. Elas se encontram no menu _Fiscal &gt; Produtos e Serviços &gt; Categorias de Produtos_ :

![](.gitbook/assets/image%20%2821%29.png)

Ou no menu _Inventário &gt; Configurações &gt; Categorias de Produtos_.

