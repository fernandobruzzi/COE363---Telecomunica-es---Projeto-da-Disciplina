# Primeiro Extrato

Simulador de carreira financeira para quem tem 16 anos ou mais. O jogador recebe uma renda mensal, toma 1 decisão por mês e escolhe o destino do saldo, até comprar o objetivo que definiu no início. O foco do projeto é ensinar educação financeira, e a parte técnica foi mantida no mínimo necessário.

## Como executar

Abra o arquivo `primeiro-extrato.html` em qualquer navegador. Não há instalação, servidor nem cadastro.

A internet é usada apenas para carregar as fontes dos títulos. Sem conexão, o jogo funciona com uma fonte padrão.

O progresso fica salvo no próprio navegador (localStorage). Limpar os dados do navegador apaga a carreira.

## Como se joga

1. Escolha um nome, uma proposta de renda e um objetivo.
2. No início de cada mês, a renda entra e as contas fixas saem.
3. Uma carta apresenta uma situação, o conceito envolvido e 3 opções. As chances de cada opção não são exibidas.
4. O resultado mostra o que mudou em cada saldo e o que a situação ensina.
5. No fim do mês, o jogador decide se separa dinheiro para lazer e para onde vai o restante (conta, reserva, ações ou metade em cada).
6. O fechamento exibe o extrato do mês e os saldos finais.

O jogador vence ao comprar o objetivo e perde se a conta fechar 3 meses seguidos no vermelho.

## Elementos de ensino

- **Conceito da rodada.** Cada carta traz a definição do conceito principal e, na primeira aparição, um exemplo numérico.
- **Botões de informação.** Os demais termos da carta podem ser abertos antes da escolha.
- **Manual.** Fica abaixo da ficha do personagem e reúne apenas os termos que já apareceram.
- **Saúde financeira.** Nota de 30 a 99, com o cálculo aberto por componente (reserva, investimentos, bem-estar, conhecimento, objetivo e dívida). Os patamares são Promessa, Titular, Destaque, Craque e Lenda.
- **Relatório final.** Lista cada decisão que fugiu do recomendado, o que era indicado e o motivo.

Os 6 primeiros meses seguem ordem fixa (orçamento, inflação, imprevisto, golpe, liquidez e ações). Depois, as cartas são sorteadas.

## Estrutura do código

O arquivo único está dividido em 3 partes, indicadas por comentários.

| Parte | Conteúdo |
|---|---|
| 1. Conteúdo | Glossário (`GLOSS`), propostas de renda (`PERFIS`), objetivos (`OBJ`), patamares (`NIVEIS`), parâmetros (`REF`) e cartas (`CARTAS`) |
| 2. Motor | Regras do jogo, sem dependência da tela (`novo`, `puxar`, `decidir`, `fecharMes`, `proximo`, `comprar`, `score`) |
| 3. Interface | Funções que desenham o estado e enviam ações ao motor |

Não há backend, banco de dados nem autenticação. Como o jogo é individual e por turnos, tudo roda no navegador, o que também evita a coleta de dados pessoais.

## Como alterar o conteúdo

**Parâmetros gerais.** Em `REF`, `cheque` é o juro mensal da conta negativa, `reserva` é o rendimento mensal líquido da reserva e `max` é o número de meses seguidos no vermelho que encerra o jogo.

**Rendas e objetivos.** Edite as listas `PERFIS` e `OBJ`.

**Glossário.** Cada termo de `GLOSS` tem título (`t`), definição (`d`) e exemplo (`e`).

**Cartas.** Cada carta de `CARTAS` tem os campos abaixo.

| Campo | Função |
|---|---|
| `tag`, `t`, `x` | Rótulo, título e narrativa |
| `termo` | Conceito principal, que deve existir em `GLOSS` |
| `mais` | Outros termos exibidos como botões de informação |
| `li` | Texto de "O que isso ensina" |
| `m` | Índices das opções recomendadas, usados no relatório final |
| `ops` | Opções, cada uma com rótulo (`r`), chance de dar certo de 0 a 100 (`p`) e os efeitos `ok` e `bad` |
| `cond`, `once`, `pre` | Condição para a carta aparecer, uso único e preparação antes de exibir |

A ordem dos primeiros meses está em `FIXAS`.

## Dados de referência

Regras reais adotadas, com base em outubro de 2026.

- Selic em torno de 14% ao ano.
- Cheque especial com teto de 8% ao mês.
- Imposto de renda regressivo na renda fixa, de 22,5% até 180 dias a 15% acima de 720 dias.
- Lucro com ações isento para vendas de até R$ 20 mil no mês e tributado em 15% acima disso.
- FGC com cobertura de até R$ 250 mil por CPF e por instituição.

Esses valores mudam com o tempo e devem ser conferidos antes de qualquer uso em sala de aula ou divulgação.

## Simplificações

- A reserva rende uma taxa líquida fixa de cerca de 0,85% ao mês, e o CDB, de cerca de 0,96%. A Selic não varia durante a partida.
- As ações são um único saldo, com variação mensal sorteada.
- A inflação é sorteada em torno de 4,5% ao ano e atinge apenas o preço do objetivo.
- Rendas, contas fixas, preços e chances das cartas são estimativas, não dados oficiais.
- A cobrança do cartão parcelado ou no rotativo é lançada inteira no mês seguinte.
- O IOF não aparece, porque cada rodada dura 1 mês.

## Limitações conhecidas

- O motor foi testado por simulação automática de 900 carreiras. A interface ainda não passou por teste sistemático em navegadores e celulares.
- O gabarito das opções recomendadas (campo `m`) foi definido na criação das cartas e merece revisão pedagógica.
- Há 15 cartas. Em carreiras longas, elas se repetem.

## Próximos passos sugeridos

- Níveis, com um novo objetivo e cartas mais avançadas a cada carreira concluída.
- Mais cartas, incluindo crédito, seguro, previdência e impostos.
- Volta da escolha de empresas e da tabela regressiva detalhada em um modo avançado.
- Testes com o público-alvo para calibrar dificuldade e linguagem.

## Aviso

Jogo educativo. As situações e empresas são fictícias e nada aqui constitui recomendação de investimento.
