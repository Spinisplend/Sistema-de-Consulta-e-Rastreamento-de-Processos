# Portal de Rastreamento de Processos Corporativos

> **Nota de Conformidade e Engenharia:** Este repositório documenta a arquitetura de um sistema corporativo real desenvolvido para um órgão governamental. Devido a políticas de integridade de dados e conformidade (NDA), o código-fonte original contendo chaves de planilhas, rotas e regras de negócio específicas é mantido em repositório privado.

## Visão Geral
Aplicação web construída na arquitetura Google Apps Script (GAS) para atuar como um portal unificado de consulta. O sistema resolve o problema de fragmentação de dados ao buscar, higienizar e consolidar o status de processos administrativos que tramitam por múltiplos departamentos e planilhas distribuídas.

## Stack Tecnológica
* **Backend:** Google Apps Script 
* **Frontend:** HTML5, CSS3, JavaScript
* **Banco de Dados:** Google Sheets API 
* **Comunicação:** `google.script.run` 

## Arquitetura e Soluções de Engenharia

### 1. Agregação de Dados Distribuídos
O banco de dados original da instituição operava de forma descentralizada em diversas planilhas gigantescas.
* O backend foi arquitetado para iterar de forma assíncrona sobre um vetor de Múltiplos IDs de Banco de Dados (Planilhas), realizando a busca do número de processo específico (Primary Key) de ponta a ponta sem onerar o tempo de resposta do cliente.

### 2. Sanitização de Dados Sujos (Regex Parsing)
Um dos maiores desafios de arquiteturas baseadas em planilhas é a entrada não padronizada de dados por operadores humanos.
* **Solução:** Implementação de algoritmos de sanitização utilizando Expressões Regulares (Regex). A função de extração varre células com textos longos e notas manuais, identifica padrões de data (dd/MM/yyyy) e extrai programaticamente a última iteração temporal válida para conversão em objetos `Date` estritos.

### 3. Motor de Cálculo de Prazos (SLA Tracking)
O sistema não apenas exibe dados estáticos, mas processa a inteligência de negócios da instituição.
* Cálculos de diferença temporal e matemática de datas são executados no backend durante o parse dos dados para determinar gargalos processuais e tempo de resposta (SLA) entre o envio e a devolutiva de diferentes setores jurídicos e administrativos.

### 4. Geração Dinâmica de Relatórios e Viewport
* Frontend otimizado para Single Page Application (SPA), onde o estado da tela muda sem recarregamento.
* Implementação de injeção de CSS específico para mídia de impressão (`@media print`), permitindo que a aplicação converta os dados renderizados no DOM em relatórios físicos formatados e limpos, isolando a interface de busca.
