Clientes
- Aumento ou redução de quantidade de plantões com status agendado ou realizado
- Focado em clientes um a um!

Quantidade de plantões cancelados pela familia
- Quantidade de cuidadores retirados por pedido do cliente
	- Motivo da mudança servico cancelado pelo cliente
- quantidade de plantoes com status cancelado pelo cliente

Quantidade de plantoes cancelados pela sanii
- Campo cancelado pela empresa (nao consegue achar alguem para mandar)


- Atraso de cuidador
	- Checkins com acima de 30 min de atraso

- Reclamação
	- Historico profissionais cliente

Retirada de cuidador
- Cliente pediu - remover cuidador da escala


Troca de cuidador nos plantões
- quantidade de incidentes criados de troca de profissionais por cliente e por plantao
- quantas trocas houve por cliente

Health score - nao temos ainda


Rotatividade: quantidade de cuidadores x escala
- 24/7 - 5 cuidadores fixas
- 12h - 2 cuidadores
- FDS - 2 ou 3
- Dia de semana intercalado - 1 
- Dia de semana seguido - 2

- heuristica
- 1 mes e meio de janela para moda

Escala fixada - profissionais que fizeram mais de um mes de plantao em dias fixos

##### 16.03.26
-> Escalas (tabela), contém toda a serie histórica
-> Checar se ha plantão e não há escala
-> falecimento, escala encerrada filtrados, realizado pelo profissional 🆗
-> padronizar `[Inativo]` 🆗
-> Cancelado por cliente,  empresa, realizado, agendado/confirmado juntos 🆗

-> detalhes lista -> grid
-> Clustering das categorias (AI)

+55 48 9171-4181 Lucia Mees -- BSV, marketing

=======================================
Checkin/checkout/categoria atraso em plantões -> de checks



Cliente Pediu - Remover Cuidador da Escala -> troca

Profissional Pediu - Sair da Escala -> troca

Mudança Solicitada pelo Profissional -> troca

Profissional Não Compareceu   ->  falta

Negado Pelo Profissional -> troca



========================

checkin/out/plantaos

========================


-- report correlation between churn and rotations
-- visao over time de rotations e em forma de porcentagem



DATA RECOMMENDATIONS

- plantoes nao sao associados a escalas!
	- Hoje: plantoes que estao dentro da data de começo e fim da escala sao associados aquela escala
	- **Não é ideal**
		- exemplo: há plantões em quintas feitas a noite dentro de uma escala segunda-quarta de manhã
		- quando há duas escalas simultâneas não temos como decidir a qual escala aquele plantão pertence.
		- No máximo dá para fazer heurísticas, mas nunca vai acertar tudo.
			- e.g.: dia da semana do plantão -> escala que abrange aquele dia/horário
			- trabalho enorme no modelo de dados para resultado mínimo (provável que menos de 10% dos casos)
			
		- *Como estou tratando hoje:* plantões são associados a TODAS as escalas daquele período, duplicando se houver duas ou mais!

	- **Ideal**:
		- Cada plantão pertence a uma escala, precisa associar essas duas tabelas no Airtable


- precisamos do ID dos clientes na tabela de CS
	- **Nome não é ideal**:
		- muitos erros de digitação
		- mesmo que nome esteja perfeito:
			- temos várias contas com mesmo nome (inativas, antigas, etc)
			- difícil de associar a reclamação a uma conta em específico (filtro de ID não funciona no gráfico de incidentes)
	- **Ideal**: ID do cliente OU url do Airtable do cliente (dá para extrair o ID)

=============
Check in > de 30min de atraso  ✅
check-out > mais de 30 min adiantado  ✅
Troca:  

- menos de 24h ou profissional novo nunca atendeu cliente ✅
- colunas a mais: notes, past partner, partner ✅

nome, data que entrou (entrevista), cnpj, risco, cancel rate, qtd plantoes realizados (geral), relacao com senior services, tipo de profissional, idade, resumo, link airtable ✅

======
dashboard clientes:

historico de cuidador: se houve reclamacao referente ao cuidador ✅
	-> neutro, negativo 

dividir entre atendimento/historico e falta/atraso/noshow ✅
nome do cuidador tabela ✅

cliente pediu para sair, profissional saiu da escala, erro interno remover da escala ✅


====
dashboard summary  ✅

no show -> no mes, mes anterior = amarelo, 3+ meses, verde  ✅

+7% amarelo; +10% -> vermelho reduçao, o.w. verde (em dias)  ✅

======

historico_profissional (neutro, negativo) ✅
neutro -> 0.5
neg -> 1
\>=1 vermelho
\>=0.5 amarelo

-> ✅
< 1 mes - 1
< 2 meses - 0.7
< 3 meses - 0.5
\>=3 - 0

========

Mar 31 26

-> Waterfall Plantões parou de funcionar ✅
-> Mutiplicador se já houve outra reclamação no passado ✅
-> Delta do score total ✅
-> Coluna extra: cliente está há 45 dias ou mais + filtro ✅
-> Incluir pessoas com menos de 30 dias, deixar variação de plantões vazio ✅
-> Categorias ✅
	0-15
	15-30
	30-45
	45-60
	60-90
	90-180
	180-365
	365+
-> manter só mẽs atual e delta ✅
-> porcentagem acima do ideal rotatividade ✅
-> ==snapshot todo dia primeiro do estado da tabela health.sql==
-> Fator que mais contribuiu no risk score ✅



##### April 9

% de plantões SEM checkin OU checkout
Pesos iguais

-> Dashboard de Cuidadores
- Mesmas métricas de CS

-> Adicionar histórico no dashboard de clientes
