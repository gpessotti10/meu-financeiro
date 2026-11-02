# 💰 Meu Financeiro

O **Meu Financeiro** é uma Single Page Application (SPA) com características de Progressive Web App (PWA). A aplicação foi desenvolvida com foco em privacidade (offline-first, client-side storage), leveza e portabilidade de dados[cite: 1].

## 🚀 Stack Tecnológica e Arquitetura
O projeto foi construído em um formato "No-Build", sem a necessidade de ferramentas como Node.js, Webpack ou Babel[cite: 1]. A aplicação inteira está contida em um único arquivo `index.html`[cite: 1].

*   **Core UI:** React 17 e ReactDOM importados via CDN[cite: 1]. O código utiliza a API nativa `React.createElement`, o que dispensa a compilação de JSX[cite: 1].
*   **Estilização:** Tailwind CSS injetado via CDN de script[cite: 1].
*   **Manipulação de Dados (I/O):** SheetJS (`xlsx`) via CDN, utilizado para a conversão bidirecional entre objetos JSON e planilhas Excel `.xlsx`[cite: 1].
*   **Persistência:** Armazenamento local utilizando a API nativa `localStorage` do navegador[cite: 1].
*   **Hospedagem:** Preparado para servidores de arquivos estáticos como GitHub Pages, Netlify ou Vercel[cite: 1].

## ⚙️ Funcionalidades Principais
*   **Dashboard Visual:** Exibe o cálculo dinâmico do fluxo de caixa e um gráfico circular (Pie Chart) renderizado de forma reativa com CSS inline dinâmico (`conic-gradient`)[cite: 1].
*   **View Analítica (Planilha):** Possui filtros compostos que combinam buscas textuais por descrição ou categoria com filtros de status da transação (todos, pendente, pago)[cite: 1]. As transações do tipo receita não utilizam controle visual de "pago"[cite: 1].
*   **Motor de Recorrência (CRUD Complexo):** Permite a edição em lote de itens recorrentes com três opções: alterar apenas o item do mês atual, atualizar toda a série de lançamentos correspondentes, ou aplicar o reajuste apenas deste mês em diante[cite: 1].
*   **Migração Anual (Forecast):** Oferece visualização consolidada de 12 meses (Janeiro a Dezembro) e uma função de "Duplicar Recorrência", que busca os itens do ano atual e os transpõe para o próximo ano gerando novos identificadores[cite: 1].
*   **Backup e Portabilidade:** O sistema exporta o estado dos lançamentos formatando um *Workbook* em `.xlsx` com o SheetJS[cite: 1]. Na importação, o arquivo é lido via `FileReader` e os dados JSON processados substituem completamente o estado anterior (Restauração Full)[cite: 1].

## 🗄️ Arquitetura de Dados
Todo o estado global é gerenciado pelo componente `<App />` e armazenado no `localStorage` em duas chaves principais[cite: 1]:
1.  `meu_financeiro_senha`: Armazena a senha de acesso como string[cite: 1].
2.  `meu_financeiro_lancamentos`: Armazena o banco de dados principal, um array de objetos JSON contendo os dados estruturados de cada transação (id, descrição, valor, tipo, categoria, data, status e flag de recorrência)[cite: 1].

O sistema não salva totais no banco; os valores totalizadores (como receitas do mês e contas pendentes) são derivados em tempo de execução por meio de métodos de array (`filter`, `reduce`) filtrados pela string de `mesAtual`[cite: 1].

## 🔒 Segurança e Privacidade
O aplicativo não utiliza criptografia avançada, e a senha funciona exclusivamente como um bloqueio da interface de usuário (UI Lock)[cite: 1]. Como os dados residem apenas na máquina local do cliente, ataques de interceptação de rede (MITM) ou vazamentos em servidores não se aplicam a esta arquitetura[cite: 1]. A opção de resetar o aplicativo aciona o comando `localStorage.clear()` para apagar toda a base de dados local permanentemente[cite: 1].

## 📱 Instalação (PWA Mobile)
O arquivo HTML contém metatags que o preparam para rodar nativamente em dispositivos móveis[cite: 1]. Ao ser adicionado à Tela de Início via Safari ou Chrome Mobile, o aplicativo funcionará em modo *Standalone* sem a barra de URL, consumindo todos os recursos diretamente do cache do navegador[cite: 1].
