# -PROJETO-1-Sales-Performance-Dashboard-Analise-de-dados
🟦 PROJETO 1 — Sales Performance Dashboard-Analise de dados - vitrine-brasil-sales-dashboard


Pensamentos para desenvolver o projeto 1: 🟦 PROJETO 1 — Sales Performance Dashboard-Analise de dados.


Aqui vai todo meu raciocínio até o final do projeto.


primeiro vou proteger o arquivo original, e criar uma outra pasta e copiar e colar esse arquivo nela e vamos trabalhar editando esse novo arquivo para não perdemos o arquivo original bruto.

Pensando como um analista, antes de fazer qualquer coisa vamos analisar todos os dados primeiro e ver se esta tudo certo, ou se tem algo errado.

Para isso eu adicionei filtros e fui filtrando e procurando inconsistências e ja achei algumas: 

Etapa 1 — Inspeção inicial

Base:
- 2.000 registros
- Período: janeiro a dezembro de 2025
- 12 colunas

Problemas identificados:
- Inconsistência de caixa em Estado
- Espaço extra em Estado
- Inconsistência de caixa em Região
- Valores ausentes em Estado/Região
- Espaço duplicado no nome de um produto

Próxima etapa:
- Tratamento e limpeza dos dados com Power Query.

EU Cliquei em qualquer lugar da tabela, e então eu fui em Dados, e depois em De Tabela/Intervalo, e ai abre o power query e cliquei primeiro na aba estados.

Transformar → Formatar → MAIÚSCULAS

agora a Etapas Aplicadas Ficaram assim: Fonte, Tipo Alterado, Texto em maiuscula, valor substituido, colocar cada palavra em maiuscula, Valor substituido 1,2 e 3 e Texto aparado

Agora analisando os dados vemos que falta algumas informações, como por exemplo o Faturamento, então vamos aproveitar o power query para adicionar uma nova coluna.

Adicionar Coluna → Coluna Personalizada

Nome da nova coluna: Faturamento
Formula da coluna: [Quantidade] * [Preço_Unitário]

Adicionar Coluna → Coluna Personalizada

Nome: Custo_Total
Formula: [Quantidade] * [Custo_Unitário]

Adicionar Coluna → Coluna Personalizada

Nome: Lucro
Formula: [Faturamento] - [Custo_Total]

Adicionar Coluna → Coluna Personalizada

Nome: Margem
Formula: [Lucro] / [Faturamento]

Depois formato o resultado para porcentagem.

Página Inicial → Fechar e Carregar → Fechar e Carregar Para...

Tabela, nova planilha.

Depois criei uma tabela dinâmica em outra planilha para analisar os valores da tabela, somando eles.

Foram criadas tabelas dinâmicas para analisar: 
Resumo geral
Por região
Por categoria
Por vendedor
Por mês


Depois fui nessas tabelas e criei um gráfico para as seguintes respectivas tabelas:
Evolução do Faturamento
Faturamento por Região
Faturamento por Categoria
Faturamento por Vendedor

Depois cliquei em cima da tabela que exportamos, fui em nova medida, e criei 5 novas medidas DAX para: Total Faturamento, Total Lucro, Total Pedidos, Unidades Vendidas.

usando as seguintes formulas:
Total Faturamento = SUM(Vendas_Tratadas1[Faturamento])
Total Lucro = SUM(Vendas_Tratadas1[Lucro])
Total Pedidos = DISTINCTCOUNT(Vendas_Tratadas1[Pedido_ID])
Unidades Vendidas = SUM(Vendas_Tratadas1[Quantidade])
Margem DAX = DIVIDE([Total Lucro], [Total Faturamento], 0)


.Depois eu fui em visualizações --> cartão --> e depois arrastei total faturamento para dentro do cartão, e repeti isso com todas as medidas principais que usamos anteriormente: 
Total Faturamento
Total Lucro 
Total Pedidos
Unidades Vendidas 
Margem DAX 


.Depois foi a hora de criar gráficos para facilitar a analise dos dados, foram criados gráficos para: Faturamento por mês, faturamento por região, faturamento por categoria e faturamento por vendedor

.Depois usei a segmentação de dados para criar filtros de região, categoria e vendedor, para analisar dados de forma individualizada.

. Agora passando pra analise de dados quando vemos os números brutos nós temos: Total faturamento: 1.82 milhoes, total lucro: 730,77 mil, total de pedidos 2 mil, unidades vendidas 4,66mil,  margem de 40,1%.

Com isso podemos tirar as seguintes informações: Temos algumas informações derivadas interessantes:
Ticket médio aproximado:
R$ 1,82 milhão ÷ 2.000 pedidos ≈ R$ 910 por pedido
Média de unidades por pedido:
4.660 ÷ 2.000 ≈ 2,33 unidades por pedido

Análise geral: A Vitrine Brasil apresentou aproximadamente R$ 1,82 milhão em faturamento em 2025, distribuídos em 2.000 pedidos e cerca de 4,66 mil unidades vendidas. O lucro calculado foi de aproximadamente R$ 730,77 mil, resultando em uma margem de 40,1%. O ticket médio aproximado foi de R$ 910 por pedido, enquanto a média foi de 2,33 unidades por pedido.

Observação: a margem deste projeto considera apenas o faturamento e o custo dos produtos presentes na base. Não estão sendo considerados despesas operacionais, impostos, frete ou outros custos empresariais.

Agora passando para uma analise mais filtrada para região vemos o seguinte: 
Análise regional: O Sudeste apresentou o maior desempenho da empresa, com R$ 604,19 mil em faturamento, representando aproximadamente 33,2% do faturamento total, além de registrar o maior número de pedidos e unidades vendidas. Sul e Nordeste apresentaram desempenhos próximos em faturamento, enquanto o Centro-Oeste apresentou o menor faturamento total.
Apesar das diferenças de volume, as margens das quatro regiões permaneceram bastante próximas, variando entre 39,8% e 40,3%. Isso indica que a principal diferença de desempenho entre as regiões está relacionada ao volume de vendas, e não a diferenças significativas de rentabilidade.
Um ponto adicional observado foi que o Centro-Oeste apresentou o maior faturamento médio por pedido, mesmo sendo a região com menor faturamento total, indicando maior valor médio das vendas realizadas nessa região.

números brutos das regiões: 604.189,82 faturamento total da região sudeste, região sul: 467.330,48 , regiao nordeste: 451.731,70 , Centro-Oeste 299.420,34 . Agora usando os filtros, começando pela regiao sudeste: Lucro: 243,05 mil, 670 pedidos, 1,57mil unidades vendidas, margem: 40,2% . Sul: Lucro: 187,33 mil, 505 pedidos, 1,19 mil unidades vendidas, 40,1 margem. Nordeste: Lucro: 179,64 , 507 pedidos, 1,15 mil vendidos, 39,8% de margem. Centro-Oeste: 120,75 mil lucro, 318 pedidos, 754 unidades vendidas, 40,3% margem.


.Analisando por categoria agora dados brutos: Agora a analise por categoria temos acessorios: 117,18 mil faturados, e 55,56 mil lucro, 299 pedidos, 693 unidades vendidas, 47,4% de margem. Eletronicos: 872,84 mil , 339,02 mil, 920 pedidos, 2,19 mil unidades vendidas, 38,8% de margem. Moveis: 801,57 mil faturamento, 318,39 mil lucro, 399 pedidos, 897 unidades vendidas, 39,7% de margem. Papelaria 31,08 mil faturados, 17,81 mil lucro, 382 pedidos, 884 unidades vendidas, 57,3% margem.

.Análise por categoria: Eletrônicos foi a principal categoria da empresa, com R$ 872,84 mil em faturamento, representando aproximadamente 47,9% da receita total, além de apresentar o maior número de pedidos, unidades vendidas e lucro absoluto. Móveis apresentou desempenho próximo em faturamento, com R$ 801,57 mil, porém com apenas 399 pedidos, indicando um valor médio por pedido significativamente maior que o de Eletrônicos.
Apesar de possuir menor participação no faturamento, Acessórios e Papelaria apresentaram margens superiores às demais categorias, com 47,4% e 57,3%, respectivamente. Papelaria apresentou a maior margem do portfólio, porém seu impacto financeiro total foi pequeno devido ao baixo faturamento.
Eletrônicos, apesar de ser a principal categoria em faturamento e lucro, apresentou a menor margem entre as categorias, com 38,8%, indicando um possível ponto de investigação relacionado aos custos, preços ou composição dos produtos.

.Analise bruta dos dados dos vendedores:
Amanda Costa: Faturamento: 200,66 mil, Lucro: 82,04 mil, Pedidos: 249, 586 unidades vendidas, 40,09% margem. Bruno Lima: Faturamento: 230,54 mil, Lucro: 91,65 mil, pedidos: 242, unidades vendidas: 574, margem: 39,08%. Camila Rocha: Faturamento: 209,31 mil, Lucro: 83,35 mil, Pedidos: 261, unidades vendidas: 587, margem : 39,08%. Diego Martins: Faturamento: 209,98 mil, Lucro: 84,82 mil, Pedidos: 240, unidades vendidas: 548, Margem: 40,4%. Eduardo Alves: Faturamento: 224,91 mil, Lucro: 89,31 mil, Pedidos: 245, Unidades vendidas: 569, Margem: 39,7%. Fernanda Silva: Faturamento: 278,32 mil, Lucro: 112,17 mil, Pedidos: 273, Unidades vendidas: 647, Margem: 40,3%. Gabriel Santos: Faturamento: 249,07 mil, Lucro: 99,08 mil, Pedidos: 258, unidades vendidas: 602, Margem: 39,8%. Helena Souza: 219,87 mil, Lucro: 88,36 mil, Pedidos: 232, Unidades Vendidas: 551, Margem: 40,2%.


.Fernanda Silva é a melhor vendedora no desempenho geral. Ela lidera em faturamento, lucro e unidades vendidas.
Diego Martins possui a maior margem: 40,4%. Portanto, ele não é o líder em faturamento, mas suas vendas são ligeiramente mais rentáveis proporcionalmente.
Também existe uma diferença interessante entre volume de pedidos e valor médio do pedido.
Fernanda teve 273 pedidos e R$ 278,32 mil de faturamento, resultando em aproximadamente R$ 1.019 por pedido.
Amanda teve 249 pedidos, mas R$ 200,66 mil de faturamento, aproximadamente R$ 806 por pedido.
Então:
A quantidade de pedidos, sozinha, não explica o faturamento. O valor médio de cada pedido também é importante.


.Análise por vendedor: Fernanda Silva apresentou o melhor desempenho geral, liderando em faturamento, lucro e unidades vendidas. Diego Martins apresentou a maior margem de lucro, apesar de não possuir o maior faturamento. A comparação também demonstrou que o número de pedidos, isoladamente, não determina o faturamento, pois o valor médio de cada pedido também influencia o resultado. As margens dos vendedores permaneceram relativamente próximas, indicando que as principais diferenças de faturamento estão relacionadas principalmente ao volume e ao valor das vendas.


.Dados Brutos de faturamento de cada mês:
Faturamento dos meses: Janeiro: 138.771,11 . Fevereiro: 135.483,70 . Março: 175.380,58 . Abril: 144.157,68 . Maio: 141.287,40 . Junho: 156.803,13 . Julho: 139.495,94 . Agosto: 183.023,99 . Setembro: 146.321,97 . Outubro: 129.356,14 . Novembro: 161.075,41 . Dezembro: 171.515,29.



.Análise mensal: O faturamento apresentou comportamento oscilante durante 2025, sem uma tendência de crescimento contínuo ao longo do ano. Agosto foi o mês de maior faturamento, com R$ 183,02 mil, enquanto outubro apresentou o menor resultado, com R$ 129,36 mil. Apesar das oscilações, o segundo semestre apresentou faturamento aproximadamente 4,4% superior ao primeiro semestre, e dezembro terminou 23,6% acima de janeiro, indicando uma recuperação no final do ano.

Ponto de atenção: A queda entre agosto e outubro merece investigação, especialmente para identificar quais regiões, categorias ou produtos contribuíram para essa redução. Os dados disponíveis neste projeto permitem identificar a queda, mas não determinar sua causa diretamente.


- CONCLUSÃO EXECUTIVA
A análise da Vitrine Brasil apresentou um faturamento total de aproximadamente R$ 1,82 milhão em 2025, distribuído em 2.000 pedidos e aproximadamente 4,66 mil unidades vendidas. O lucro calculado foi de R$ 730,77 mil, resultando em uma margem geral de aproximadamente 40,1%.
Em relação às regiões, o Sudeste apresentou o maior desempenho, com aproximadamente R$ 604,19 mil em faturamento, representando cerca de 33,2% do faturamento total. A análise mostrou que as margens das regiões foram bastante próximas, variando de 39,8% a 40,3%, indicando que as principais diferenças de resultado estão relacionadas principalmente ao volume de vendas. O Centro-Oeste, apesar de apresentar o menor faturamento total, apresentou o maior faturamento médio por pedido.
Na análise por categoria, Eletrônicos foi a principal categoria, com aproximadamente R$ 872,84 mil em faturamento, representando cerca de 47,9% da receita total, além de liderar em pedidos, unidades vendidas e lucro absoluto. Móveis apresentou faturamento próximo ao de Eletrônicos, porém com quantidade de pedidos consideravelmente menor, indicando um valor médio por pedido mais elevado.
Papelaria apresentou a maior margem, com 57,3%, seguida por Acessórios, com 47,4%. Entretanto, essas categorias possuem participação muito menor no faturamento total. Já Eletrônicos, apesar de liderar em faturamento e lucro absoluto, apresentou a menor margem entre as categorias, com 38,8%, representando um possível ponto de investigação relacionado a custos, preços ou composição dos produtos.
Na análise dos vendedores, Fernanda Silva apresentou o melhor desempenho geral, liderando em faturamento, lucro e unidades vendidas. Diego Martins apresentou a maior margem, com 40,4%, apesar de não possuir o maior faturamento. As margens dos vendedores permaneceram relativamente próximas, indicando que as diferenças de faturamento estão relacionadas principalmente ao volume e ao valor médio dos pedidos.
Na análise temporal, o faturamento apresentou comportamento oscilante ao longo de 2025, sem crescimento contínuo. Agosto foi o melhor mês, com R$ 183,02 mil, enquanto outubro apresentou o menor resultado, com R$ 129,36 mil. Apesar das oscilações, o segundo semestre apresentou faturamento aproximadamente 4,4% superior ao primeiro, e dezembro terminou aproximadamente 23,6% acima de janeiro.
Principais pontos de atenção e oportunidades de investigação: a queda de faturamento entre agosto e outubro merece uma investigação mais detalhada para identificar quais produtos, categorias ou regiões contribuíram para essa redução. Além disso, as categorias Papelaria e Acessórios apresentam margens elevadas, enquanto Eletrônicos concentra grande parte da receita, mas possui margem inferior, o que pode justificar análises adicionais sobre custos, preços e composição do mix de produtos.
Limitações da análise: os dados utilizados são fictícios e foram criados exclusivamente para fins de portfólio. Além disso, a margem calculada considera somente os custos dos produtos presentes na base, não incluindo despesas como impostos, frete, salários, marketing ou outras despesas operacionais.

