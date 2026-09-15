# Valores fiscais — Registo de Horas & Vencimento

Fonte de dados usada pela app "Registo de Horas & Vencimento" para o salário mínimo nacional e as tabelas de retenção na fonte de IRS. A app descarrega [`valores-fiscais.json`](valores-fiscais.json) ao abrir; se não conseguir (sem internet, ficheiro em falta), usa os últimos valores conhecidos e avisa o utilizador.

## Atualizar quando sair uma tabela nova

1. Editar `valores-fiscais.json`:
   - `atualizadoEm`: data da publicação (AAAA-MM-DD)
   - `fonte`: referência do despacho/diploma
   - `smn`: novo salário mínimo nacional
   - `tabelaI` / `tabelaII` / `tabelaIII`: um item por escalão, na ordem do despacho
     - `ate`: limite superior da remuneração mensal do escalão (`null` no último escalão, sem limite)
     - `taxa`: taxa marginal de retenção
     - `parcelaFixa`: parcela a abater (quando é um valor fixo)
     - `formula`: só nos escalões "de transição" em que a parcela depende da remuneração — `parcela = taxa × fator × (referencia − remuneração)`. Usar exatamente um de `parcelaFixa` ou `formula` por escalão.
     - `adicional`: parcela adicional a abater, por dependente
2. Confirmar que o JSON é válido (ex.: colar em [jsonlint.com](https://jsonlint.com)) e fazer commit/push para `master`.
3. A app volta a descarregar automaticamente na próxima vez que abrir com internet — não é preciso publicar uma nova versão da app.
