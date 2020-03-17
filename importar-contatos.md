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

{% hint style="info" %}
A relação pai/filho mais frequente nos objetos 'Contatos' é entre uma empresa 'pai' e um empregado 'filho'. Mas é bom anotar que os endereços \(tipo endereço para envio ou endereço de cobrança\) são também registrados como objetos '_Contato_' no banco de dado do Odoo.

Então para importar endereços específicos de um contato é preciso **primeiro importar o contato 'pai' e depois importar o endereço 'filho'** desse contato \(cf o campo "type" do arquivo Excel de importação\)
{% endhint %}

Segue uma lista dos campos interessantes para uma importação de Contatos com todas as relações possíveis :

<table>
  <thead>
    <tr>
      <th style="text-align:left">T&#xED;tulo coluna</th>
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
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>name</b>
      </td>
      <td style="text-align:left">Nome do Contato</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>legal_name</b>
      </td>
      <td style="text-align:left">Nome completo do Contato</td>
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
      <td style="text-align:left">Escolher entre :
        <br />- &quot;Contato&quot;
        <br />- &quot;Endere&#xE7;o de Cobran&#xE7;a&quot;
        <br />- &quot;Endere&#xE7;o para envio:&quot;
        <br />- &quot;Endere&#xE7;o privado&quot;
        <br />- &quot;Outro endere&#xE7;o&quot;
        <br />
        <br />Uma pessoa f&#xED;sica ou uma empresa ser&#xE1; sempre to tipo &quot;Contato&quot;.
        As outras op&#xE7;&#xF5;es s&#xE3;o para registrar v&#xE1;rios tipos de
        endere&#xE7;os. Pensar em primeiro importar o contato &apos;pai&apos; (com
        &apos;type&apos; igual a &quot;Contato&quot;) antes de importar os endere&#xE7;os
        &apos;filhos&apos; (com outro valor de &apos;type&apos;)</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>parent_id/id</b>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>country_id</b>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>lang</b>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>category_id/id</b>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>property_product_pricelist/id</b>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>property_account_position_id/id</b>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>property_account_receivable_id/id</b>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>property_account_payable_id/id</b>
      </td>
      <td style="text-align:left"></td>
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
      <td style="text-align:left">compte bancaire</td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table> 

