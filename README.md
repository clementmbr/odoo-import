# Funcionamento

A complexidade da importação de dados no Odoo vem da complexidade em registrar em Odoo **as ligações** entre os objetos importados.

Por exemplo, um dos campos de um _Contato_ é o campo dos _Marcadores_ \(ou "categoria de contato"\). Entendemos que teremos que importar todos os _Marcadores_ primeiro antes de importar os _Contatos_, e durante a importação dos _Contatos_ teremos que indicar os _**External ID**_ dos _Marcadores_  de cada _Contato_ importado.

O _External ID_, chamado também de _**XML ID**_, é o identificador de um objeto presente em Odoo. Ele permite permite fazer a diferença entre

