---
description: ...com o módulo `l10n_br_fiscal` da Akretion instalado
---

# Importar produtos

O módulo [l10n\_br\_fiscal](https://github.com/akretion/l10n-brazil/tree/12.0-mig-l10n_br_account_product/l10n_br_fiscal) desenvolvido pela [Akretion](https://akretion.com/pt-BR) permite ter no Odoo **a integralidade das informações fiscais necessárias** ao cadastramento oficial de qualquer tipo de produto, incluindo o NCM, NBS, NBM, CEST e outros :

![](.gitbook/assets/image%20%2810%29.png)

Como qualquer outro objeto Odoo, o processo para importar produtos é de [primeiro **exportar** alguns produtos](importar-contatos.md#importacoes-anteriores-aos-contatos) atuais com a lista dos campos que você deseja importar, com a opção "_Update data \(import-compatible export\)_" e o formato Excel.

![](.gitbook/assets/image%20%2830%29.png)

A importação da quantidade de produtos deve ser realizado num segundo tempo, importando um _Ajuste de Estoque._

## Produtos e Variantes

Existe **dois tipos de objetos Odoo** distintos para a gestão dos produtos, registrados em duas tabelas distintas no banco de dados : 

* **product.product** para as variantes de um mesmo produto \(criados pelo menu _Variantes de Produto_\)
* **product.template** para os diferentes produtos que podem ter cada um várias variantes \(criados pelo menu _Produtos_\) :

![](.gitbook/assets/image%20%2823%29.png)

Por padrão esse menu das _Variantes de Produto_ não aparece no Odoo, tem que ser ativado nas configurações do modulo _Inventário_ :

![](.gitbook/assets/image%20%2815%29.png)

Porém, mesmo quando essa opção não for selecionada e o menu não aparecer, **os dois tipos de objetos coexistem** : quando criar um objeto _product.template_ pelo menu _Produtos_ clássico, um objeto _product.product_ será **automaticamente criado** e ligado a esse _product.template_, sendo a "única variante" dele.

E vice e versa, quando uma variante _product.product_ é criada de zero pelo menu _Variantes de Produto_, o seu produto _product.template_ relacionado é criado automaticamente, sendo um _product.template_ com uma única variante.

Por isso, é muito importante entender que quando você importar produtos pelo **botão "Importar" do menu** _**Produtos**_, você vai criar objetos do tipo ****_**product.template**_ \(e os objetos _product.product_ relacionados serão criados automaticamente\) enquanto quando importar produtos pelo **botão "Importar" do menu** _**Variantes de Produtos**_, você vai criar objetos do tipo _**product.product**_ \(e objetos _product.template_ serão criados automaticamente\).

{% hint style="warning" %}
Se quiser importar uma lista de novos produtos junto com as suas quantidades no inventário, você precisa primeiro importar a lista de produtos e depois importar um **Ajuste de Estoque**.

No arquivo excel do _Ajuste de Estoque_ importado, você deve **indicar o** _**External ID**_ **do objeto** _**product.product**_ **do produto**, além da sua quantidade e da sua locação no inventário.

Por isso **recomendamos importar a lista dos novos produtos pelo menu** _**Variantes de Produto**_, mesmo se você não usar essa gestão dos variantes depois. No arquivo excel dessa importação você vai indicar os _External IDs_ desses novos objetos _product.product_... o que vai permitir você citar esses mesmos _External IDs_ na importação do _Ajuste de Estoque_ na seguida.
{% endhint %}

Apesar de adicionar um certa complexidade, essa gestão dos produtos com esses dois tipos de objetos é muito bem elaborada no Odoo.

Os campos comuns aos _product.template_ e _product.product_ são **sincronizados** \(e.g. se modificar o nome de um _product.product_ o nome do seu _product.template_ relacionado vai ser modificado automaticamente, e vice e versa\).

Ao contrário, os campos do tipo "**atributo**" de um _product.product_ **não vão estar ligados** com campos do seu objeto _product.template_ correspondente porque eles vão "caracterizar" essa variante \(e. g. o campo "cor" de um objeto "mesa", ou o campo "tamanho" de um objeto "camisa"\).

Graça a essa sincronização dos campos comuns, os nomes das colunas do arquivo excel de importação \(i.e. os "campos" desses produtos importados\) vão ser **as mesmas** se usar esse arquivo para importar objetos _product.product_ ou _product.template_.

A única coisa é de cuidar de **não realizar a importação em duplo !** Se importar objetos _product.product_, os objetos _product.template_ relacionados vão ser criados automaticamente. Isso quer dizer que você vai escolher e conhecer os _External IDs_ desses _product.product_ importados, porém você não vai conhecer facilmente os _External IDs_ desses _product.template_. Eles vão ser **diferentes** e definidos automaticamente por Odoo. __

## Campos para importar

É possível importar apenas a lista de campos que você precisa, porém alguns campos são obrigatórios e devem ser informados como :

* o Nome
* o Tipo
* a Categoria
* o Tipo Fiscal
* a origem do ICMS
* o NCM
* e o Gênero Fiscal

Nessa ideia, uma lista  mínima de campos para exportar e preparar o seu arquivo Excel para importação seria essa :

![](.gitbook/assets/image%20%2824%29.png)

Observando a questão de [importar os _External ID_ dos objetos que jà existem](./#como-importar-relacoes-entre-objetos) no Odoo para realizar a conexão com o seu novo produto importado.

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
      <td style="text-align:left"><b>default_code</b>
      </td>
      <td style="text-align:left">
        <p>Refer&#xEA;ncia interna do produto (opcional).</p>
        <p>Geralmente &#xE9; um n&#xFA;mero &#xFA;nico do <em>Produto</em> para diferenciar
          dois produtos que poderiam ter o mesmo nome.</p>
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
        um tipo de objeto Odoo que permite tratar juntos os <em>Produtos</em> da
        mesma categoria (como para necessidades cont&#xE1;beis por exemplo)</td>
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
</table>

[Baixar aqui um exemplo de arquivo excel de importação de produtos.](https://drive.google.com/file/d/1m7SbjiW-sgme3Jj4CuXtKquEj2iiQKhC/view?usp=sharing)

### Categoria de Produto

É preciso primeiro definir essas Categorias e depois exportá-las com o seu External ID. Elas se encontram no menu _Fiscal &gt; Produtos e Serviços &gt; Categorias de Produtos_ :

![](.gitbook/assets/image%20%2821%29.png)

Ou no menu _Inventário &gt; Configurações &gt; Categorias de Produtos_.

### Tipo Fiscal

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
Esses _Tipos Fiscais_ são fixos no Odoo, **não é possível modificá-los**.
{% endhint %}

### Origem do ICMS

Escolher o número seguindo a Origem do ICMS desejado :

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
Essas _Origens de ICMS_ são fixas no Odoo, **não é possível modificá-las**.
{% endhint %}

## Importar um Ajuste de Estoque

Para definir a **quantidade** de vários produtos presentes num estoque no Odoo é preciso realizar uma operação de _Ajuste de Estoque :_

![](.gitbook/assets/image%20%2819%29.png)

Em vez de definir esse _Ajuste de Estoque_ manualmente, é possível importar um. Isso ajuda muito se conhecer os _External IDs_ dos produtos cuja quantidade vai ser definida, por exemplo depois da importação prévia desses produtos.

Os campos mínimos necessários para importar um _Ajuste de Estoque_ são os seguintes :

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
        <p><em>External ID</em> dado ao <em>Ajuste de Estoque</em> importado.</p>
        <p>Se deixar vazio o Odoo criar&#xE1; um automaticamente.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>name</b>
      </td>
      <td style="text-align:left">Nome do <em>Ajuste de Estoque</em> importado.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>line_ids/location_id/id</b>
      </td>
      <td style="text-align:left"><em>External ID</em> da Local do Estoque a onde vai se encontrar uma certa
        quantidade de um certo <em>Produto</em>.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>line_ids/product_id/id</b>
      </td>
      <td style="text-align:left">
        <p>&#x26A0;&#xFE0F; <em>External ID</em> do objeto <b>product.product</b> do <em>Produto</em> cuja
          quantidade vai ser definida.</p>
        <p></p>
        <p>Corresponde ao <em>External ID </em>definido no arquivo excel de importa&#xE7;&#xE3;o
          dos produtos <b>apenas</b> se esse arquivo foi importado pelo bot&#xE3;o
          &quot;Importar&quot; do menu <a href="importar-produtos.md#produtos-e-variantes"><em><b>Variantes de Produto</b></em></a>.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>line_ids/product_qty</b>
      </td>
      <td style="text-align:left">
        <p>A quantidade do <em>Produto</em> no <em>Local</em>.</p>
        <p></p>
        <p>Pensar em definir a <em>Unidade de Medida</em> do <em>Produto</em> se precisar.</p>
      </td>
    </tr>
  </tbody>
</table>

[Baixar aqui um exemplo de arquivo excel de importação de ajuste de estoque.](https://drive.google.com/file/d/1_vq57UVlzdcRKtTr3RHbDsIqF_hkHzdG/view?usp=sharing)



