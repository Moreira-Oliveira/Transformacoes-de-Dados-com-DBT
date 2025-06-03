# Transformacoes-de-Dados-com-DBT

# O Que é Transformação de Dados?

Transformação de dados é o processo de converter, organizar ou modificar dados de um formato bruto ou original para um formato mais adequado e útil para análise, armazenamento ou uso em sistemas específicos.
Esse processo é essencial na engenharia de dados, especialmente em pipelines de ETL (Extract, Transform, Load – Extração, Transformação e Carga) ou ELT (Extract, Load, Transform – Extração, Carga e Transformação).


# principais aspectos da Transformação de Dados

🔹 1. Qualidade dos Dados

* Correção de erros: como valores inválidos, inconsistentes ou fora de padrão.

* Remoção de duplicidades: eliminar registros redundantes.

* Tratamento de dados ausentes (nulls): preenchimento, exclusão ou substituição por valores padrão.


🔹 2. Padronização e Normalização

* Uniformização de formatos: datas no mesmo padrão, textos em caixa baixa, etc.

* Normalização numérica: escalonamento de valores (ex: entre 0 e 1) para análises ou modelos.


🔹 3. Conversão de Tipos de Dados

* Transformar tipos como string para inteiro, data, booleano, etc., de acordo com o uso final.


🔹 4. Agregações e Cálculos

* Resumos estatísticos: média, soma, contagem, máximo/mínimo.

* Colunas derivadas: novos campos criados com base em fórmulas (ex: lucro = receita - custo).


🔹 5. Enriquecimento de Dados

* Inserção de informações complementares, como dados geográficos ou demográficos, via junções com outras fontes.


🔹 6. Filtragem e Seleção

* Isolamento de registros relevantes com base em regras de negócio ou critérios de análise.


🔹 7. Mapeamento e Substituição de Valores

* Troca de códigos por descrições legíveis (ex: 1 → "Ativo", 0 → "Inativo").

* Reclassificação ou agrupamento de categorias.


🔹 8. Integração de Dados

* Combinar informações de múltiplas fontes (bancos de dados, planilhas, APIs, etc.) em um único dataset coerente.


🔹 9. Ordem e Estrutura

* Reorganização das colunas ou registros conforme a necessidade (ex: ordenação por data).

* Transformações de formatos (ex: de JSON para tabela relacional).


🔹 10. Automação e Reprodutibilidade

* Garantir que a transformação possa ser reproduzida automaticamente em pipelines com ferramentas como dbt, Airflow, Spark, Pandas, entre outras.


# Aplicações práticas


Aqui estão algumas aplicações práticas da transformação de dados em diferentes contextos do mundo real. Cada exemplo mostra como esse processo é essencial para análise, tomada de decisão e eficiência operacional:


📊 1. Business Intelligence (BI)

Contexto: Uma empresa quer analisar as vendas mensais por região.

Transformações realizadas:

* Conversão de datas para o formato padrão (YYYY-MM).

* Junção de tabelas de vendas com dados de regiões e produtos.

* Agregação da receita por mês e por região.

* Criação de uma coluna de margem de lucro (receita - custo).

Ferramentas usadas: SQL, Power BI, Tableau


🛒 2. E-commerce

Contexto: Identificar os clientes com maior valor de compra nos últimos 6 meses.

Transformações realizadas:

* Filtragem de transações nos últimos 180 dias.

* Conversão de valores monetários para o mesmo padrão de moeda.

* Agrupamento por cliente e soma do valor gasto.

* Ordenação e classificação dos top clientes.

Ferramentas usadas: Python (pandas), SQL, dbt


🏥 3. Saúde

Contexto: Integrar dados de pacientes vindos de diferentes hospitais.

Transformações realizadas:

* Padronização de formatos de data e nomes de campos.

* Normalização de unidades (ex: peso em kg, temperatura em °C).

* Tratamento de dados ausentes e inconsistentes (ex: datas inválidas).

* Mapeamento de códigos de doenças para descrições.

Ferramentas usadas: Spark, Apache NiFi, Python


🏦 4. Setor Financeiro

Contexto: Calcular risco de crédito com base no histórico de transações.

Transformações realizadas:

* Criação de colunas derivadas como: média de gastos mensais, padrão de atraso de pagamento.

* Enriquecimento com dados externos (ex: score de crédito).

* Normalização de dados para alimentar modelos preditivos.

Ferramentas usadas: Python, PySpark, SQL, Scikit-learn


🚚 5. Logística

Contexto: Otimizar rotas de entrega com base no histórico de atrasos.

Transformações realizadas:

* Conversão de timestamps em tempo total de entrega.

* Cálculo da média e desvio padrão por rota.

* Identificação de padrões com maior probabilidade de atraso.

* Enriquecimento com dados de trânsito e clima.

Ferramentas usadas: Python, Pandas, GeoPandas, APIs externas


🎓 6. Educação

Contexto: Avaliar desempenho de alunos por disciplina.

Transformações realizadas:

* Junção de notas, frequência e atividades em uma única tabela.

* Cálculo de médias ponderadas por matéria.

* Categorização do desempenho (ex: "Excelente", "Regular", "Ruim").

* Filtragem de alunos com risco de reprovação.

Ferramentas usadas: SQL, Excel, Power BI


# Criação de Macros, Refatoramento e Deplay em Produção com DBT

📚 Preparaando a Máquina Cliente com DBT

Usaremos um script para criar uma imagem de container personalizada. Ele define um ambiente pronto para desenvolvimento e execução de projetos dbt (Data Build Tool) com SQLite, dentro de um container.


🔧 Etapas detalhadas do que ele faz:


1. Escolha da base da imagem:

* A imagem começa com uma versão enxuta do Python 3.11, chamada python:3.11-slim, que já vem com o interpretador Python instalado.


2. Identificação do mantenedor:

* Um rótulo (LABEL) é adicionado para identificar quem mantém essa imagem. Neste caso, o nome informado é "DSA" (possivelmente Data Science Academy ou um usuário).


3. Instalação de ferramentas básicas do sistema operacional:

* Atualiza a lista de pacotes do sistema.

* Instala ferramentas úteis como:

🔹 build-essential: para compilar pacotes Python que tenham código nativo (C/C++).

🔹 git: para controle de versão.

🔹 vim e nano: editores de texto dentro do terminal.

🔹 sqlite3: o sistema de banco de dados local que será usado com o dbt.

* Após a instalação, limpa os arquivos temporários para manter a imagem enxuta.


4. Criação de diretório e volume:

* Cria o diretório /dsa, que servirá como o local principal de trabalho no container.

* Define este diretório como um volume Docker, o que significa que ele pode ser sincronizado com a máquina host. Isso é útil para salvar dados ou projetos mesmo após o container ser parado.


5. Definição do diretório de trabalho:

* Define /dsa como o diretório onde todos os comandos futuros dentro do container serão executados. É como fazer cd /dsa no terminal.


6. Instalação do dbt com suporte ao SQLite:

* Instala o dbt-core, que é o núcleo da ferramenta dbt.

* Instala o dbt-sqlite, que é o adaptador necessário para que o dbt possa se conectar a bancos de dados SQLite.


7. Exposição de porta (opcional):

* A porta 8080 é exposta para permitir que algum serviço futuro (como um dashboard ou servidor) possa ser acessado externamente se for configurado.


8. Comando padrão:

* Define o /bin/bash como o comando a ser executado quando o container iniciar. Isso significa que, ao rodar o container, o usuário será levado a um terminal bash para poder interagir diretamente com o ambiente.


![image](https://github.com/user-attachments/assets/305d17a7-c14f-477d-b223-145967006ef5)


📚 Criando o Projeto DBT e Configurando os targets

![image](https://github.com/user-attachments/assets/a8898a1e-abd4-4e93-97c9-2c063cf0ae2e)

* Vamos criar um ambiente com dev e prod usando SQLite. Criar modelos, rodar transformações, aplicar testes e gerar documentação.

Seguindo o paso a paso do projeto teremos esse resultado (paso a paso na paasta):

![image](https://github.com/user-attachments/assets/6ac5472e-f46a-48bc-917c-daed913c1a59)

Verificando o debug:

![image](https://github.com/user-attachments/assets/b47fbf1f-d5d4-45ab-b74a-434ff104136b)


📚 Deploy dos Modelos de Dados Iniciais

Vamos passar os Models que estou disponibilizando para a pasta que foi criada. Primeiro vamos passar o modelo de Venda e o de Cliente. Após vamos para o Docker e executar o comando dbt run.

🔍 O que está acontecendo (Cçiente):

1. {{ config(materialized='view') }}

* Informa ao dbt que este modelo será materializado como uma view, ou seja:

    * O dbt criará uma view no banco de dados ao invés de uma tabela física.

    * A view sempre trará dados atualizados diretamente da tabela tb_clientes.

2. WITH clientes_base AS (...)

* Cria uma CTE (Common Table Expression) chamada clientes_base com todos os dados da tabela tb_clientes.

3. SELECT final:

* Retorna os campos cliente_id, nome, cidade e estado da CTE clientes_base.

📌 Resumo:

Esse modelo cria uma view no banco com os dados completos de clientes, extraídos diretamente de tb_clientes.


🔍 O que está acontecendo (Vendas):

1. {{ config(materialized='view') }}

* Novamente, dbt criará uma view em vez de uma tabela materializada.

2. CTE vendas_base

* Carrega os dados da tabela tb_vendas, mas filtra apenas as vendas com valor inferior a R$ 500.

3. SELECT final:

* Seleciona os campos principais de cada venda com valor menor que 500: venda_id, cliente_id, data_venda, valor.

📌 Resumo:

Esse modelo cria uma view com vendas de baixo valor (menos de R$ 500), útil para análises específicas ou filtragem de dados antes de cálculos posteriores.

Resultado da Criação
![image](https://github.com/user-attachments/assets/4ef71638-f24d-48cf-bb34-3313e537b2b8)


📚 Deploy do Modelo Maart

Na pasta "models" vamos criar a pasta "mart" e passar os modelos paraa ele:

![image](https://github.com/user-attachments/assets/c4ba440d-c208-4b5c-8e16-d7121b812939)

![image](https://github.com/user-attachments/assets/c6fed001-1c1f-437c-b979-769919c5cd3f)
OBS:Teremos que mudar o nome conforme aparrece

🔍 Como resultado

Este modelo dbt:

Combina os dados dos modelos clientes e vendas usando o cliente_id.

Filtra os clientes apenas dos estados SP e RJ.

Calcula o total de vendas por cliente.

📌 Resultado final:

Você terá uma tabela (provavelmente uma view, dependendo da configuração {{ config(...) }} no topo do arquivo) com a seguinte estrutura:

![image](https://github.com/user-attachments/assets/b5a594e2-336f-4add-ae66-412863cbdc45)


📚 Construção da Macro

Da mesma forma como fizemos com os models e os mart, vamos transferir asa macros para a pasta que foi criada. 

* E para que elas serrvem: 

Para reutilizar lógica SQL em múltiplos modelos, promovendo refatoração e padronização.

Onde uma calcula a média apenas das vendas com valor menor que 450.

🔍 Explicação passo a passo:

{{ valor }}: é um argumento da macro — você passa o nome da coluna ao chamá-la (por exemplo, valor).

CASE WHEN {{ valor }} < 450 THEN {{ valor }} ELSE NULL END:
Essa expressão substitui valores maiores ou iguais a 450 por NULL, que são ignorados pela função AVG().

Resultado: uma média condicional, baseada apenas em valores abaixo de 450.

E a outra soma os valores de uma coluna. É basicamente um atalho para SUM(...).

🔍 Explicação:

{{ valor }} é o nome da coluna que você vai somar.

SUM({{ valor }}) executa a soma dos valores dessa coluna no SQL.


![image](https://github.com/user-attachments/assets/d91be7a5-4c68-435d-ac58-450289b43039)


✅ Conclusão

Ao longo deste material, exploramos os principais fundamentos e práticas de transformação de dados, um pilar essencial na engenharia de dados moderna. Desde a garantia da qualidade e padronização dos dados até a integração, agregação e enriquecimento das informações, cada etapa do processo contribui diretamente para a criação de pipelines mais eficientes, escaláveis e confiáveis.

Utilizando o dbt (Data Build Tool), vimos como é possível estruturar transformações com clareza, versionamento e reprodutibilidade. Por meio de CTEs, modelos materializados como views, e a construção de marts analíticos, organizamos os dados de forma lógica e eficiente. Além disso, introduzimos macros reutilizáveis, facilitando a padronização de cálculos e promovendo a manutenção do código.

Na prática, construímos um ambiente controlado com SQLite dentro de um container Docker, onde criamos modelos de clientes e vendas, aplicamos filtros e junções, e produzimos uma visão analítica consolidada com foco em regiões específicas. Também mostramos como estruturar o projeto dbt com separação entre ambientes de desenvolvimento e produção.

Esse tipo de abordagem torna o dbt uma ferramenta extremamente poderosa para projetos de dados modernos, especialmente em contextos de ELT, onde a transformação ocorre após a carga dos dados. Além disso, ao aplicar os conceitos aprendidos em setores como varejo, saúde, logística e finanças, reforçamos a aplicabilidade real e o impacto da transformação de dados nas decisões estratégicas das organizações.

Por fim, com a adoção de boas práticas como modularização de modelos, uso de macros personalizadas, e organização por camadas (staging, marts, etc.), estamos construindo não apenas transformações, mas plataformas de dados robustas, auditáveis e escaláveis.

