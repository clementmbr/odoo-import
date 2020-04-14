# Importar contatos

O video oficial da Odoo S.A. é um bom primeiro passo caso estiver descobrindo a organização dos _Contatos_ no Odoo :

{% embed url="https://youtu.be/BDcVuozHrOg" %}

O único campo obrigatório para a criação de um Contato é o _Nome_, por isso é teoricamente possível importar um arquivo com apenas uma lista de nomes e criar facilmente centenas de Contatos.

Porém, vários outros tipos de objetos Odoo apontam em direção a objetos do tipo _Contato_. Por isso, como a gente indicou na introdução, é necessário [importar primeiramente todos esses objetos antes de finalmente importar os Contatos](./#como-importar-relacoes-entre-objetos) indicando o _External ID_ de cada objeto com qual cada _Contato_ estará relacionado.

## Importações anteriores aos Contatos

Segue a lista exaustiva dos objetos Odoo a ser importados antes da importação de Contatos, indicando cada vez a onde encontrar esse objeto na interface de Odoo.

{% hint style="info" %}
[Como a gente indicou na introdução](./#criacao-do-external-id-durante-a-importacao), não esquecer de escolher/escrever o _External ID_ de cada objeto importado para controlar e conhecer o nome desses _External ID_ antes de reutilizá-los no arquivo Excel de importação dos _Contatos_.
{% endhint %}

### Bancos

Menu _Contatos &gt; Configuração &gt; Bancos_ :

![](.gitbook/assets/image%20%283%29.png)

Entendemos que um _Contato_ vai estar ligado a um _Banco_ e uma _Conta Bancária_ vai estar ligada a ambos um _Banco_ e um _Contato_. Por isso é preciso importar nesta ordem :

1. Os Bancos
2. Os Contatos
3. As [Contas Bancárias](importar-contatos.md#contas-bancarias)

### Condições de Pagamento

Menu _Faturamento &gt; Configuração &gt; Condições de Pagamento :_

![](.gitbook/assets/image%20%2830%29.png)

### Posições Fiscais

Uma _Posição Fiscal_ é uma tabela que faz a relação entre uma taxa e uma outra taxa. Cf o nosso [tutorial sobre as Posições Fiscais](https://odoo-doc.gitbook.io/fonctionnel/-LxRKpKPmg6E8oIFl-4d/v/pt/faturamento/posicoes-fiscais).

É possível definir ou encontrar a lista das _Posições fiscais_ no menu _Faturamento &gt; Configuração :_

![](.gitbook/assets/image%20%2814%29.png)

### Lista de preços

Uma "_Lista de preço_" é o nome de objeto Odoo enganosamente escolhido para diferenciar vários "Grupos de clientes" e vender um produto a preços diferentes para cada grupo. Cf o nosso [tutorial sobre as _"Listas de preço"_](https://odoo-doc.gitbook.io/fonctionnel/-LxRKpKPmg6E8oIFl-4d/v/pt/vendas/lista-de-precos).

É possível definir ou encontrar a lista dessas "_Lista de preços_" clicando embaixo da opção "_Múltiplos Preços de Venda por Produto_" nas _Configurações_ do aplicativo de Vendas :

![](.gitbook/assets/image%20%2812%29.png)

### Marcadores de Contato \(ou "Tags do Contato", ou "categoria de Contato"\)

Seguir as etapas que a gente viu [na introdução](./#criacao-do-external-id-durante-a-importacao) para realizar a importação de _Marcadores_.

### Tratamento para o contato \(ou "Título"\)

Para indicar se um _Contato_ estará chamado de _Senhor_, _Senhora_ ou _Doutor_, é necessário preencher o campo "Título" do _Contato_, selecionando o _Título_ desejado dentro de uma lista de objetos Odoo existentes.

Para importar esses objetos do tipo _Título_, ir no menu _Contatos &gt; Configuração &gt; Tratamento para o contato_.

![](.gitbook/assets/image%20%2810%29.png)

### Contas de Recebimento e de Pagamento

Uma Conta de Recebimento \(respectivamente de Pagamento\) corresponde à **Conta do** _**Plano de Contas**_ da Contabilidade da sua empresa usada para registrar um recebimento \(resp. pagamento\) de dinheiro desse Contato :

![](.gitbook/assets/image%20%282%29.png)

{% hint style="info" %}
Esses campos de "Lançamentos Contábeis" aparecem na aba "Faturamento" dos Contatos são visíveis apenas se a opção "**Mostrar Todas as Funcionalidades de Contabilidade**" for selecionada na lista dos direitos de acesso do seu usuário.

Esse lista se modifica na ficha do próprio usuário no menu _Configurações &gt; Utilizadores e Empresas &gt; Usuários_, com o [modo "desenvolvedor" ativado](https://odoo-development.readthedocs.io/en/latest/odoo/usage/debug-mode.html).
{% endhint %}

Geralmente as empresas usam as mesmas Contas de Recebimento e de Pagamento para todos os clientes e essas Contas estão dadas automaticamente para todos os novos clientes \(criados manualmente ou durante um importação\).

Isso quer dizer que **você não precisa fazer nada** \(nem precisa mencionar as colunas desses campos no arquivo Excel de importação\) caso você quiser usar essas Contas padrões para os seus contatos. A única coisa é pensar em instalar o módulo Odoo correspondente ao Plano de Contas desejado **antes** de importar os Contatos. 

Por exemplo, para usar um Plano de Contas padrão para empresas do Simples Nacional, instalar o módulo da OCA [l10n\_br\_simple](https://github.com/OCA/l10n-brazil/tree/12.0/l10n_br_simple).

Caso você quiser indicar uma Conta de Recebimento ou Pagamento especial para um Contato particular, é só preencher a coluna **property\_account\_receivable\_id/id** ou **property\_account\_payable\_id/id** do arquivo Excel de importação dos Contatos com o valor do _External ID_ da Conta desejada, encontrada no menu _Faturamento &gt; Configurações &gt; Plano de Contas_ :

![](.gitbook/assets/image%20%2822%29.png)

## Importação dos contatos

[Como explicamos na introdução](./#relacao-pai-filho), é importante realizar em primeiro a importação dos Contatos "pai" \(como uma empresa\) e depois os Contatos "filho" \(como os membros de uma empresa\) ligados aos Contatos "pai" pelo External ID desses.

{% hint style="info" %}
A relação pai/filho mais frequente nos objetos 'Contatos' é entre uma empresa 'pai' e um empregado 'filho'. Mas é bom anotar que os endereços \(como o endereço para envio ou o endereço de cobrança\) são também registrados como objetos '_Contato_' no banco de dado do Odoo.

Então para importar endereços específicos de um contato é preciso **primeiro importar o contato 'pai' e depois importar o endereço 'filho'** desse contato \(cf o campo "type" do arquivo Excel de importação\)
{% endhint %}

Segue uma lista dos campos interessantes para uma importação de Contatos com todas as relações possíveis com os outros objetos Odoo :

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
        <p><em>External ID</em> dado ao contato importado.</p>
        <p>Se deixar vazio o Odoo criar&#xE1; um automaticamente.</p>
        <p></p>
        <p>&#xC9; importante preencher manualmente esse campo para os contatos &apos;pai&apos;.
          O <em>External ID</em> definido nesse momento ser&#xE1; usado num segundo
          tempo durante a importa&#xE7;&#xE3;o dos contatos &apos;filhos&apos;.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>name</b>
      </td>
      <td style="text-align:left">Nome usual do Contato</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>legal_name</b>
      </td>
      <td style="text-align:left">Raz&#xE3;o Social do Contato se for uma empresa, Nome completo do Contato
        se for uma pessoa f&#xED;sica</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>title/id</b>
      </td>
      <td style="text-align:left"><em>External ID</em> do <a href="importar-contatos.md#tratamento-para-o-contato">tratamento do contato</a> (T&#xED;tulo
        do contato)</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>is_company</b>
      </td>
      <td style="text-align:left">Campo Booleano : &apos;1&apos; se for uma empresa, &apos;0&apos; se n&#xE3;o
        for</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>customer</b>
      </td>
      <td style="text-align:left">Campo Booleano : &apos;1&apos; se for um cliente, &apos;0&apos; se n&#xE3;o
        for</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>supplier</b>
      </td>
      <td style="text-align:left">Campo Booleano : &apos;1&apos; se for um fornecedor, &apos;0&apos; se
        n&#xE3;o for</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>active</b>
      </td>
      <td style="text-align:left">Campo Booleano : &apos;1&apos; se for um contato ativo, &apos;0&apos;
        se n&#xE3;o for</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>type</b>
      </td>
      <td style="text-align:left">
        <p>Escolher entre :</p>
        <ul>
          <li>&quot;Contato&quot;</li>
          <li>&quot;Endere&#xE7;o de Cobran&#xE7;a&quot;</li>
          <li>&quot;Endere&#xE7;o para envio:&quot; <em>(com os &quot;:&quot; no final)</em>
          </li>
          <li>&quot;Endere&#xE7;o privado&quot;</li>
          <li>&quot;Outro endere&#xE7;o&quot;</li>
        </ul>
        <p><b>Uma pessoa f&#xED;sica ou uma empresa ser&#xE1; sempre com &apos;type&apos; igual a &quot;Contato&quot;</b>.
          As outras op&#xE7;&#xF5;es s&#xE3;o para registrar v&#xE1;rios tipos de
          endere&#xE7;os de um contato. Pensar em primeiro importar esse contato
          &apos;pai&apos; (com &apos;type&apos; igual a &quot;Contato&quot;) antes
          de importar os endere&#xE7;os &apos;filhos&apos; (com o valor de &apos;type&apos;
          escolhido)</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>parent_id/id</b>
      </td>
      <td style="text-align:left"><em>External ID</em> do contato &apos;pai&apos; do contato importado</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>country_id/id</b>
      </td>
      <td style="text-align:left">
        <p><em>External ID</em> do pa&#xED;s do contato. Por exemplo &quot;<b>base.br</b>&quot;
          para o Brasil ou &quot;<b>base.us</b>&quot; para os Estados Unidos.</p>
        <p></p>
        <p>Para acessar &#xE0; lista completa de todos os <em>External ID </em>dos
          pa&#xED;ses registrados no banco de dado do Odoo, ir na p&#xE1;gina dos
          objetos do tipo &quot;Pa&#xED;s&quot; pelo menu <em>Contatos</em> &gt; <em>Configura&#xE7;&#xE3;o</em> &gt; <em>Pa&#xED;ses</em>,
          e <b>exportar</b> os pa&#xED;ses desejados com o seu respectivo nomes e <em>External ID</em>.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>state_id/id</b>
      </td>
      <td style="text-align:left">
        <p><em>External ID</em> do estado do contato. Por exemplo &quot;<b>base.state_br_rj</b>&quot;
          para o Rio de Janeiro ou &quot;<b>base.state_br_sp</b>&quot; para S&#xE3;o
          Paulo.</p>
        <p></p>
        <p>Para acessar &#xE0; lista completa de todos os <em>External ID </em>dos
          estados registrados no banco de dado do Odoo, ir na p&#xE1;gina dos objetos
          do tipo &quot;Estado&quot; pelo menu <em>Contatos</em> &gt; <em>Configura&#xE7;&#xE3;o</em> &gt; <em>Estados</em>,
          e <b>exportar</b> os estados desejados com os seus respectivos nomes e <em>External ID</em>.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>lang</b>
      </td>
      <td style="text-align:left">
        <p><em>C&#xF3;digo de Pa&#xED;s/L&#xED;ngua </em>do idioma do contato. &quot;<b>pt_BR</b>&quot;
          se for portugu&#xEA;s do brasil, &quot;<b>en_US</b>&quot; se for ingl&#xEA;s
          americano.</p>
        <p></p>
        <p>Para acessar &#xE0; lista completa de todos os <em>C&#xF3;digo de Pa&#xED;s/L&#xED;ngua</em> dos
          idiomas registrados no banco de dado do Odoo, ir na p&#xE1;gina dos objetos
          do tipo &quot;Idioma&quot; pelo menu <em>Configura&#xE7;&#xF5;es</em> &gt; <em>Tradu&#xE7;&#xF5;es</em> &gt; <em>Idiomas</em>,
          e <b>exportar</b> os idiomas desejados com os seus respectivos nomes e <em>C&#xF3;digo de Pa&#xED;s/L&#xED;ngua.</em>
        </p>
        <p></p>
        <p>Esse <em>C&#xF3;digo de Pa&#xED;s/L&#xED;ngua</em> n&#xE3;o &#xE9; para
          ser confundido com o <em>C&#xF3;digo ISO</em> ou o <em>External ID </em>do
          idioma !</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>category_id/id</b>
      </td>
      <td style="text-align:left"><em>External ID </em>dos <a href="importar-contatos.md#marcadores-de-contato-ou-tags-do-contato-ou-categoria-de-contato">Marcadores do Contato</a>.
        <br
        />
        <br />Para dar v&#xE1;rios Marcadores ao mesmo contato, <a href="https://www.odoo.com/documentation/user/12.0/general/base_import/import_faq.html#how-can-i-import-a-many2many-relationship-field-e-g-a-customer-that-has-multiple-tags">informar todos os <em>External ID</em> desejados separados por uma coma &quot;,&quot; sem espa&#xE7;o</a>.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>property_product_pricelist/id</b>
      </td>
      <td style="text-align:left"><em>External ID </em>da &quot;<a href="importar-contatos.md#lista-de-precos"><em>Lista de pre&#xE7;o</em></a>&quot;
        do Contato.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>property_account_position_id/id</b>
      </td>
      <td style="text-align:left"><em>External ID </em>da <em>&quot;</em><a href="importar-contatos.md#posicoes-fiscais"><em>Posi&#xE7;&#xE3;o Fiscal</em></a><em>&quot; </em>do
        Contato.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>property_account_receivable_id/id</b>
      </td>
      <td style="text-align:left">
        <p><em>External ID </em>da &quot;<a href="importar-contatos.md#contas-de-recebimento-e-de-pagamento"><em>Conta de Recebimento</em></a>&quot;
          do Contato.</p>
        <p></p>
        <p>Pensar em importar o <em>Plano de Contas</em>  <b>antes</b> da importa&#xE7;&#xE3;o
          dos contatos e importar essa coluna apenas se n&#xE3;o usar a <em>Conta de Recebimento</em> padr&#xE3;o.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>property_account_payable_id/id</b>
      </td>
      <td style="text-align:left">
        <p><em>External ID </em>da &quot;<a href="https://app.gitbook.com/@odoo-doc/s/import-data-in-odoo/~/drafts/-M4tT1ghfGa51WXctEO8/v/pt/importar-contatos#contas-de-recebimento-e-de-pagamento"><em>Conta de Pagamento</em></a>&quot;
          do Contato.</p>
        <p></p>
        <p>Da mesma maneira, pensar em importar o <em>Plano de Contas</em>  <b>antes</b> da
          importa&#xE7;&#xE3;o dos contatos e importar essa coluna apenas se n&#xE3;o
          usar a <em>Conta de Pagamento</em> padr&#xE3;o.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>property_payment_term_id/id</b>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>property_supplier_payment_term_id/id</b>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>customer_payment_mode_id/id</b>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>supplier_payment_mode_id/id</b>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>bank_ids/id</b>
      </td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>##  Importação posteriores aos contatos

Todos os objetos que precisam estar ligados a um contato, como por exemplo as Contas Bancarias :

### Contas Bancárias

![](.gitbook/assets/image%20%286%29.png)

### 

