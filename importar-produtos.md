---
description: ...com o módulo `l10n_br_fiscal` da Akretion instalado
---

# Importar produtos

O módulo [l10n\_br\_fiscal](https://github.com/akretion/l10n-brazil/tree/12.0-mig-l10n_br_account_product/l10n_br_fiscal) desenvolvido pela [Akretion](https://akretion.com/pt-BR) permite ter no Odoo **a integralidade dos categorias fiscais necessárias** ao cadastramento oficial de qualquer tipo de produto, incluindo o NCM, NBS, NBM, CEST e outros :

![](.gitbook/assets/image%20%2810%29.png)

Como qualquer outro objeto Odoo, o processo para importar produtos é de [primeiro **exportar** alguns produtos](importar-contatos.md#importacoes-anteriores-aos-contatos) atuais com a lista dos campos que você deseja importar, com a opção "_Update data \(import-compatible export\)_" e o formato Excel.

![](.gitbook/assets/image%20%2828%29.png)

É possível importar a lista de campos que você precisar, porém alguns campos são obrigatórios e devem ser importados :

* o Nome
* o Tipo
* a Categoria
* o Tipo Fiscal
* a origem do ICMS
* o NCM
* e o Gênero Fiscal





