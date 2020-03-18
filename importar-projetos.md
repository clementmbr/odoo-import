# Importar projetos

{% hint style="info" %}
Para facilitar o processo de importação, é necessário instalar no mínimo ambos :

* o aplicativo "Projeto" \(`project`\) a base da gestão de projetos
* e "Task Logs" \(`hr_timesheet`\) para a gestão do tempo nos projetos

É apenas quando os dois módulos estiverem instalados que a visão em "lista" dos projetos é possível, [permitindo a exportação dos projetos atuais](./#external-id-na-exportacao).
{% endhint %}

## Importar o projeto

Como qualquer outro objeto Odoo, o processo para importar um projeto é de [primeiro exportar alguns projetos](importar-contatos.md#importacoes-anteriores-aos-contatos) atuais com a lista dos campos que você deseja importar com a opção "_Update data \(import-compatible export\)_" e o formato Excel.

![](.gitbook/assets/image%20%2817%29.png)

Entendemos que **um** _**Projeto**_ **é composto de** _**Tarefas**_, por isso, como para qualquer importação de objetos Odoo relacionados, é importante importar primeiro os _Projetos_ e num segundo tempo as _Tarefas_, [cada _Tarefa_ sendo relacionada ao seu _Projeto_ pelo _External ID_ do _Projeto_](./#como-importar-relacoes-entre-objetos).

Uma lista de campos interessante para importar pode ser :

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
        <p><em>External ID</em> dado ao <em>Projeto</em> importado.</p>
        <p>Se deixar vazio o Odoo criar&#xE1; um automaticamente.</p>
        <p></p>
        <p>&#xC9; importante preencher manualmente esse campo para controlar e conhecer
          o valor desse <em>External ID</em>. Ele ser&#xE1; <a href="./#como-importar-relacoes-entre-objetos">usado num segundo tempo durante a importa&#xE7;&#xE3;o das <em>Tarefas</em></a>.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>name</b>
      </td>
      <td style="text-align:left">Nome do <em>Projeto</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>user_id/id</b>
      </td>
      <td style="text-align:left">
        <p><em>External ID</em> do <em>Gerente do Projeto</em> (um <em>Usu&#xE1;rio</em> de
          Odoo)</p>
        <p>&lt;em&gt;&lt;/em&gt;</p>
        <p>Para conhecer-lo acessar &#xE0; pagina dos usu&#xE1;rios pelo menu <em>Configura&#xE7;&#xF5;es</em> &gt; <em>Utilizadores e Empresas</em> &gt; <em>Usu&#xE1;rios</em> e
          <a
          href="./#external-id-pela-interface">seguir as instru&#xE7;&#xF5;es da introdu&#xE7;&#xE3;o.</a>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>partner_id/id</b>
      </td>
      <td style="text-align:left"><em>External ID</em> do <em>Cliente do Projeto</em> (um <em>Contato</em> de
        Odoo)</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>analytic_account_id/id</b>
      </td>
      <td style="text-align:left">
        <p><em>External ID</em> da <em>Conta Anal&#xED;tica do Projeto</em>
        </p>
        <p>&lt;em&gt;&lt;/em&gt;</p>
        <p>As <em>Contas Anal&#xED;ticas</em> se encontram no menu <em>Faturamento</em> &gt; <em>Configura&#xE7;&#xE3;o</em> &gt; <em>Contas Anal&#xED;ticas</em>.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>privacy_visibility</b>
      </td>
      <td style="text-align:left">
        <p>Escolher entre :</p>
        <ul>
          <li>&quot;followers&quot;</li>
          <li>&quot;employees&quot;</li>
          <li>&quot;portal&quot;</li>
        </ul>
        <p><a href="importar-projetos.md#sobre-a-privacidade">Confere a significa&#xE7;&#xE3;o desses 3 campos</a>
        </p>
      </td>
    </tr>
  </tbody>
</table>### Sobre as Contas Analíticas

Odoo cria uma _Conta Analítica_ com o mesmo nome que o _Projeto_ **automaticamente** cada vez que você criar um _Projeto_ manualmente ou quand você importa um _Projeto_ sem preencher a coluna "_analytic\_account\_id/id_".

Então você precisa criar uma _Conta Analítica_ previamente e informar o valor do _External ID_ dessa conta no arquivo de importação de projeto **apenas** se você quiser relacionar dois projetos \(ou mais\) com a mesma _Conta Analítica_.

Se o menu _Contas Analíticas_ não aparecer no menu _Faturamento_ &gt; _Configuração_, pensar em ativar a configuração "_Contabilidade Analíticas_" do seu usuário, acessando pelo menu _Configurações_ &gt; _Utilizadores e Empresas_ &gt; _Usuários_, sem esquecer de [ativar o modo desenvolvedor](./#external-id-pela-interface) para todos os campos aparecerem.

![](.gitbook/assets/image%20%2816%29.png)

### Sobre a privacidade

Esse campo detém a visibilidade das tarefas ou incidências que pertencem ao projeto :

* '**followers**' = 'Somente convidados' : Empregados podem ver somente os projetos seguidos, tarefas ou incidências
* '**employees**' = 'Visível por todos os empregados' : Empregados podem ver todos os projetos, tarefas e incidências
* '**portal**' = 'Visível pelos clientes que seguem' : empregados veem tudo. Se o website está ativado, usuários do portal podem ver projetos, tarefas e incidências que são seguidas por eles ou alguém de sua companhia

## Importar as Tarefas

Além de relacionar uma _Tarefa_ a um _Projeto_ é necessário relacionar cada _Tarefa_ a um _**Estágio**_ de andamento.

Para encontrar o [_External ID_](./#external-id-pela-interface) __ dos Estágios, ir no menu _Projetos_ &gt; _Configuração_ &gt; _Estágios :_

![](.gitbook/assets/image%20%287%29.png)

Segue uma lista de campos para importar _Tarefas_ de _Projetos_ :

<table>
  <thead>
    <tr>
      <th style="text-align:left">T&#xED;tulo da coluna</th>
      <th style="text-align:left">Conte&#xFA;do</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><b>id</b>
      </td>
      <td style="text-align:left">
        <p><em>External ID</em> dado &#xE0; <em>Tarefa</em> importada.</p>
        <p>Se deixar vazio o Odoo criar&#xE1; um automaticamente.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>name</b>
      </td>
      <td style="text-align:left">Nome da <em>Tarefa</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>planned_hours</b>
      </td>
      <td style="text-align:left">N&#xFA;mero de horas planejadas para a realiza&#xE7;&#xE3;o da <em>Tarefa</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>user_id/id</b>
      </td>
      <td style="text-align:left">
        <p><em>External ID</em> do <em>Gerente do Projeto</em> (um <em>Usu&#xE1;rio</em> de
          Odoo)</p>
        <p>&lt;em&gt;&lt;/em&gt;</p>
        <p>Para conhecer-lo acessar &#xE0; pagina dos usu&#xE1;rios pelo menu <em>Configura&#xE7;&#xF5;es</em> &gt; <em>Utilizadores e Empresas</em> &gt; <em>Usu&#xE1;rios</em>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>project_id/id</b>
      </td>
      <td style="text-align:left"><em>External ID </em>do<em> Projeto</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>stage_id/id</b>
      </td>
      <td style="text-align:left"><em>External ID </em>do<em> Est&#xE1;gio </em>de andamento</td>
    </tr>
  </tbody>
</table>{% hint style="info" %}
Caso importar uma _Tarefa_ com um _Estágio_ que existe mas que não é presente no _Projeto_ específico da _Tarefa_, o _Estágio_ aparecerá daqui em diante nesse _Projeto_.
{% endhint %}









