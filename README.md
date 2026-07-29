
# Otimização Inteligente de Sistema de Bombeamento com Programação Inteira Mista

<p align="justify">Este projeto apresenta a otimização de um sistema de bombeamento de água considerando simultaneamente decisões hidráulicas, operacionais e econômicas. O problema consiste em determinar a melhor estratégia de operação de uma estação elevatória, buscando minimizar o custo diário total enquanto são respeitadas as restrições de demanda, capacidade das bombas, disponibilidade de equipamentos e características da tubulação.</p>

<p align="justify">Diferentemente de modelos tradicionais que consideram apenas a vazão como variável contínua, este projeto incorpora decisões discretas que representam escolhas reais de engenharia. Entre elas estão a seleção do diâmetro comercial da tubulação, a quantidade de bombas em operação e a decisão de quais equipamentos devem permanecer ligados em cada horário do dia.</p>

<p align="justify">Além do consumo energético, o modelo considera o investimento necessário para implantação da tubulação. Dessa forma, o problema deixa de ser apenas uma otimização operacional e passa a representar um problema de planejamento integrado entre custo de operação e custo de infraestrutura.</p>

---

# 1. Contexto do Problema

<p align="justify">Sistemas de bombeamento são responsáveis pelo transporte de água entre diferentes níveis de armazenamento, sendo utilizados em abastecimento urbano, processos industriais, irrigação e diversas aplicações de engenharia.</p>

<p align="justify">A operação desses sistemas envolve um equilíbrio entre diferentes fatores. A utilização de vazões elevadas reduz o tempo necessário para transportar água, porém aumenta as perdas hidráulicas e a potência exigida pela bomba. Por outro lado, a utilização de vazões menores reduz o consumo instantâneo, mas pode exigir mais horas de operação para atender a demanda diária.</p>

<p align="justify">Outro fator importante é o diâmetro da tubulação. Tubulações maiores apresentam menor perda de carga e reduzem o consumo energético ao longo da operação, porém possuem maior custo inicial de instalação. Tubulações menores possuem menor custo de implantação, mas aumentam a resistência hidráulica do sistema.</p>

<p align="justify">Portanto, existe um conflito entre investimento inicial, custo energético e estratégia operacional. A solução ótima representa o melhor compromisso econômico entre essas variáveis.</p>

---

# 2. Objetivo do Projeto

<p align="justify">O objetivo principal é desenvolver um modelo matemático capaz de determinar a configuração de menor custo para um sistema de bombeamento considerando:</p>

<p align="justify">- escolha do diâmetro comercial da tubulação;</p>

<p align="justify">- programação horária das bombas;</p>

<p align="justify">- variação do preço da energia elétrica ao longo do dia;</p>

<p align="justify">- atendimento da demanda diária de água;</p>

<p align="justify">- minimização do custo total composto por energia, operação das bombas e investimento em infraestrutura.</p>

---

# 3. Representação do Sistema

<p align="justify">O sistema considerado possui um reservatório inferior, uma estação de bombeamento, uma tubulação de transporte e um reservatório superior localizado a uma determinada altura geométrica.</p>

<p align="justify">A bomba deve fornecer energia suficiente para vencer a diferença de nível entre os reservatórios e as perdas de carga provocadas pelo escoamento na tubulação.</p>

<br>

<p align="center">

  <img src="https://github.com/rodfloripa/Projeto89/blob/main/fig1.jpg">
</p>



<br>

<p align="justify">A figura apresenta os seguintes elementos:</p>

<p align="justify">- reservatório inferior;</p>

<p align="justify">- conjunto de bombas;</p>

<p align="justify">- tubulação de recalque;</p>

<p align="justify">- reservatório superior;</p>

<p align="justify">- altura geométrica $H_g$;</p>

<p align="justify">- vazão bombeada $Q$.</p>

---

# 4. Variáveis de Decisão

<p align="justify">O problema possui variáveis contínuas e discretas. Essa combinação permite representar de forma mais realista as decisões presentes em um sistema de bombeamento industrial.</p>

## 4.1 Vazão Horária

<p align="justify">A vazão bombeada em cada hora do dia é representada pela variável contínua:</p>

$$
Q_h
$$

<p align="justify">onde $h$ representa cada uma das 24 horas do período analisado.</p>

<p align="justify">A variável $Q_h$ determina quanto volume de água será transportado em cada intervalo de operação.</p>

---

## 4.2 Estado das Bombas

<p align="justify">A operação das bombas é representada por uma variável binária:</p>

$$
u_{h,i}
\in
\{0,1\}
$$

<p align="justify">onde:</p>

<p align="justify">$u_{h,i}=1$ indica que a bomba $i$ está ligada na hora $h$.</p>

<p align="justify">$u_{h,i}=0$ indica que a bomba permanece desligada.</p>

<p align="justify">Essa variável permite que o algoritmo escolha automaticamente a quantidade de bombas necessárias em cada período.</p>

---

## 4.3 Seleção do Diâmetro

<p align="justify">O diâmetro da tubulação é uma variável discreta porque, na prática, são utilizados valores comerciais disponíveis no mercado.</p>

<p align="justify">A escolha é representada por:</p>

$$
z_j \in \{0,1\}
$$

<p align="justify">onde cada variável indica se determinado diâmetro comercial foi selecionado.</p>

<p align="justify">A restrição garante que somente uma alternativa seja escolhida:</p>

$$
\sum_j z_j = 1
$$

---

# 5. Dados do Sistema

<p align="justify">O estudo utiliza um sistema hidráulico hipotético baseado em parâmetros típicos de engenharia.</p>

| Parâmetro | Valor |
|---|---:|
| Massa específica da água | 1000 kg/m³ |
| Gravidade | 9,81 m/s² |
| Eficiência da bomba | 75% |
| Altura geométrica | 30 m |
| Comprimento da tubulação | 1000 m |
| Demanda diária | 400 m³/dia |
| Número máximo de bombas | 3 |
| Vazão mínima por bomba | 0,005 m³/s |
| Vazão máxima por bomba | 0,020 m³/s |

---

# 6. Diâmetros Comerciais Avaliados

<p align="justify">O modelo avalia diferentes opções de diâmetro para identificar o melhor equilíbrio entre investimento inicial e consumo energético.</p>

| Diâmetro | Custo aproximado |
|---|---:|
| 150 mm | R$ 300/m |
| 200 mm | R$ 450/m |
| 250 mm | R$ 650/m |
| 300 mm | R$ 900/m |

<p align="justify">O diâmetro escolhido influencia diretamente o comportamento hidráulico do sistema, pois tubulações maiores reduzem a perda de carga, porém apresentam maior custo de implantação.</p>

---

# 7. Tarifação Horária de Energia

<p align="justify">O custo da energia elétrica varia ao longo do dia. Para representar essa característica, o modelo considera diferentes tarifas horárias.</p>

<p align="justify">Durante o horário de ponta, a energia possui custo maior, criando um incentivo econômico para deslocar o bombeamento para períodos de menor tarifa.</p>

A tarifa utilizada é:

$$
Tarifa_h =
\begin{cases}
1,20, & 18 \leq h \leq 20\\
0,50, & demais\ horários
\end{cases}
$$

<p align="justify">Essa característica aumenta a complexidade do problema, pois a melhor estratégia pode não ser simplesmente operar continuamente, mas sim concentrar o bombeamento em horários economicamente mais favoráveis.</p>

# 8. Modelo Hidráulico

<p align="justify">O comportamento hidráulico do sistema é determinado pela relação entre vazão, perda de carga e altura total que a bomba precisa fornecer. A energia necessária para transportar a água depende tanto da diferença de nível entre os reservatórios quanto das perdas provocadas pelo escoamento na tubulação.</p>

---

# 8.1 Perda de Carga na Tubulação

<p align="justify">A perda de carga representa a energia dissipada devido ao atrito entre a água e as paredes internas da tubulação. Ela depende principalmente da vazão, do comprimento da tubulação, do diâmetro e das propriedades hidráulicas do sistema.</p>

<p align="justify">Neste projeto foi utilizada uma aproximação baseada na relação inversa entre perda de carga e diâmetro da tubulação:</p>

$$
h_f(Q,D)=K(D)Q^2
$$

<p align="justify">O coeficiente hidráulico depende do diâmetro escolhido:</p>

$$
K(D)\propto \frac{1}{D^5}
$$

<p align="justify">Dessa forma, quando o diâmetro aumenta, a resistência ao escoamento diminui e consequentemente a energia necessária para o bombeamento também reduz.</p>

---

# 8.2 Altura Total Manométrica

<p align="justify">A altura total manométrica representa a energia por unidade de peso que deve ser fornecida pela bomba para realizar o transporte da água.</p>

$$
H(Q,D)=H_g+h_f(Q,D)
$$

<p align="justify">Substituindo a expressão da perda de carga:</p>

$$
H(Q,D)=H_g+K(D)Q^2
$$

<p align="justify">A altura geométrica permanece constante, pois depende da diferença física entre os reservatórios. Entretanto, a parcela referente às perdas hidráulicas aumenta com a vazão.</p>

---

# 8.3 Potência da Bomba

<p align="justify">A potência requerida pela bomba depende da massa específica da água, da gravidade, da vazão, da altura manométrica e da eficiência do equipamento.</p>

$$
P=
\frac{\rho g QH}{\eta}
$$

<p align="justify">Para obter a potência em quilowatts:
</p>

$$
P_{kW}=
\frac{\rho g QH}{\eta \cdot 1000}
$$

<p align="justify">Como a altura depende da vazão, a potência possui comportamento não linear. Vazões elevadas podem provocar aumento significativo do consumo devido ao crescimento da perda de carga.</p>

---

# 9. Formulação da Função Objetivo

<p align="justify">O objetivo do modelo é minimizar o custo total diário do sistema de bombeamento. Esse custo é formado por três componentes principais:</p>

<p align="justify">1. Custo de energia elétrica;</p>

<p align="justify">2. Custo fixo de operação das bombas;</p>

<p align="justify">3. Custo de investimento da tubulação convertido em custo diário.</p>

A função objetivo completa é:

$$
\min Custo_{total}
$$

onde:

$$
Custo_{total}=
Custo_{CAPEX}
+
\sum_{h=1}^{24}
(
Custo_{energia,h}
+
Custo_{bombas,h}
)
$$

---

# 9.1 Custo de Energia

<p align="justify">O custo energético considera a potência utilizada em cada hora e a tarifa correspondente ao período.</p>

$$
Custo_{energia,h}=
P_{kW,h}
\cdot
Tarifa_h
$$

<p align="justify">A tarifa variável cria um incentivo para que o algoritmo evite operar durante horários de energia mais cara.</p>

---

# 9.2 Custo das Bombas

<p align="justify">Cada bomba em operação possui um custo fixo diário associado à manutenção e disponibilidade operacional.</p>

$$
Custo_{bombas,h}=
C_{fixo}
\sum_i u_{h,i}
$$

<p align="justify">A variável binária define automaticamente quantas bombas devem permanecer ligadas em cada horário.</p>

---

# 9.3 Custo de Investimento da Tubulação

<p align="justify">O custo inicial da tubulação depende do comprimento instalado e do diâmetro escolhido.</p>

$$
CAPEX=
L
\cdot
Custo_{m}(D)
$$

<p align="justify">Como o objetivo é comparar custos diários de operação, o investimento é amortizado considerando uma vida útil de 20 anos.</p>

$$
Custo_{CAPEX,dia}=
\frac{CAPEX}
{365 \cdot 20}
$$

---

# 10. Restrições do Modelo

<p align="justify">Além de minimizar o custo, o algoritmo deve respeitar as limitações físicas e operacionais do sistema.</p>

---

# 10.1 Escolha Única do Diâmetro

<p align="justify">Somente um diâmetro comercial pode ser escolhido:</p>

$$
\sum_j z_j=1
$$

<p align="justify">Essa restrição representa uma decisão discreta de engenharia.</p>

---

# 10.2 Atendimento da Demanda

<p align="justify">O volume bombeado durante o dia deve ser suficiente para atender a necessidade do sistema.</p>

$$
\sum_{h=1}^{24}
Q_h
\cdot
3600
\geq
Demanda
$$

<p align="justify">O fator 3600 converte horas para segundos, permitindo utilizar a vazão em metros cúbicos por segundo.</p>

---

# 10.3 Limite de Operação das Bombas

<p align="justify">A vazão horária deve respeitar a capacidade dos equipamentos instalados.</p>

$$
Q_{min}
\sum_i u_{h,i}
\leq
Q_h
\leq
Q_{max}
\sum_i u_{h,i}
$$

<p align="justify">Essa restrição impede que o modelo utilize vazões incompatíveis com a quantidade de bombas selecionada.</p>

---

# 10.4 Funcionamento Mínimo

<p align="justify">Para garantir atendimento contínuo da demanda, o modelo considera que pelo menos uma bomba deve permanecer ativa durante os períodos analisados.</p>

$$
\sum_i u_{h,i}\geq1
$$

---

# 11. Natureza Combinatória do Problema

<p align="justify">O problema apresenta características de otimização inteira mista porque combina variáveis contínuas e decisões discretas.</p>

<p align="justify">As variáveis contínuas representam grandezas físicas como vazão e potência. As variáveis inteiras representam decisões como ligar ou desligar bombas e escolher um diâmetro comercial.</p>

<p align="justify">Essa combinação produz uma superfície de custo com diferentes regiões possíveis, criando vários mínimos locais associados às diferentes combinações de operação.</p>

---

# 12. Existência de Múltiplos Mínimos

<p align="justify">A presença de variáveis discretas cria diferentes estratégias possíveis para o sistema.</p>

<p align="justify">Um exemplo seria:</p>

<p align="justify">**Estratégia 1:** Tubulação menor com baixo investimento inicial, porém maior consumo energético devido à maior perda de carga.</p>

<p align="justify">**Estratégia 2:** Tubulação maior com alto investimento inicial, mas menor consumo durante toda a operação.</p>

<p align="justify">**Estratégia 3:** Diâmetro intermediário combinado com bombeamento concentrado em horários de menor tarifa.</p>

<p align="justify">O algoritmo busca a combinação que apresenta o menor custo total, identificando o mínimo global dentro do conjunto de soluções possíveis.</p>

---

# 13. Método Computacional

<p align="justify">O problema foi implementado utilizando a biblioteca CVXPY, que permite modelar problemas de otimização matemática de forma estruturada.</p>

<p align="justify">As variáveis binárias são resolvidas através de um algoritmo de programação inteira mista. Para problemas maiores, solvers comerciais como GUROBI podem apresentar desempenho superior.</p>

<p align="justify">A solução encontrada fornece simultaneamente:</p>

<p align="justify">- diâmetro ótimo da tubulação;</p>

<p align="justify">- programação horária das bombas;</p>

<p align="justify">- perfil de vazão;</p>

<p align="justify">- custo energético;</p>

<p align="justify">- custo total diário.</p>

# 14. Implementação Computacional

<p align="justify">A implementação computacional foi desenvolvida em Python utilizando a biblioteca CVXPY para modelagem do problema de otimização inteira mista. A estrutura do código foi organizada para representar um sistema real de bombeamento, permitindo a tomada de decisões hidráulicas e econômicas simultaneamente.</p>

<p align="justify">O modelo considera um horizonte de planejamento de 24 horas, no qual o algoritmo decide automaticamente a programação das bombas, a vazão em cada período e o diâmetro comercial mais adequado para a tubulação.</p>

---

# 14.1 Bibliotecas Utilizadas

<p align="justify">As principais bibliotecas utilizadas no desenvolvimento foram:</p>

<p align="justify">- CVXPY: construção e resolução do problema de otimização;</p>

<p align="justify">- NumPy: manipulação de vetores e cálculos matemáticos;</p>

<p align="justify">- Pandas: organização dos resultados em tabelas;</p>

<p align="justify">- Matplotlib: geração das visualizações gráficas.</p>

---

# 14.2 Estrutura do Modelo Computacional

<p align="justify">O algoritmo segue as seguintes etapas:</p>

<p align="justify">1. Definição dos parâmetros físicos e econômicos do sistema;</p>

<p align="justify">2. Criação das variáveis de decisão contínuas e binárias;</p>

<p align="justify">3. Inserção das restrições hidráulicas e operacionais;</p>

<p align="justify">4. Construção da função objetivo de custo total;</p>

<p align="justify">5. Resolução através do solver de otimização;</p>

<p align="justify">6. Extração da solução ótima;</p>

<p align="justify">7. Geração das análises gráficas.</p>

---

# 15. Resultados Obtidos

<p align="justify">Após a execução do modelo, são obtidas informações completas sobre a estratégia ótima de operação do sistema.</p>

<p align="justify">Os principais resultados fornecidos pelo algoritmo são:</p>

<p align="justify">- diâmetro comercial selecionado;</p>

<p align="justify">- custo diário total;</p>

<p align="justify">- custo energético;</p>

<p align="justify">- custo operacional das bombas;</p>

<p align="justify">- custo diário equivalente do investimento da tubulação;</p>

<p align="justify">- vazão bombeada em cada hora;</p>

<p align="justify">- número de bombas em funcionamento por período;</p>

<p align="justify">- potência requerida;</p>

<p align="justify">- altura manométrica do sistema.</p>

---

# 15.1 Tabela de Operação Horária

<p align="justify">A tabela abaixo apresenta o planejamento operacional determinado pelo algoritmo de otimização.</p>

## Perfil de Operação de 24 Horas

| Hora | Tarifa (R$/kWh) | Vazão (m³/s) | Bombas Ligadas | Bomba Ativa | Potência (kW) | Altura Total (m) | Custo Energia (R$) |
|---:|---:|---:|---:|:---:|---:|---:|---:|
| 0 | 0.50 | 0.015 | 1 | B1 | 5.89 | 30.0 | 2.94 |
| 1 | 0.50 | 0.000 | 0 | Nenhuma | 0.00 | 30.0 | 0.00 |
| 2 | 0.50 | 0.015 | 1 | B2 | 5.89 | 30.0 | 2.94 |
| 3 | 0.50 | 0.015 | 1 | B3 | 5.89 | 30.0 | 2.94 |
| 4 | 0.50 | 0.015 | 1 | B1 | 5.89 | 30.0 | 2.94 |
| 5 | 0.50 | 0.015 | 1 | B2 | 5.89 | 30.0 | 2.94 |
| 6 | 0.50 | 0.000 | 0 | Nenhuma | 0.00 | 30.0 | 0.00 |
| 7 | 0.50 | 0.015 | 1 | B3 | 5.89 | 30.0 | 2.94 |
| 8 | 0.50 | 0.015 | 1 | B1 | 5.89 | 30.0 | 2.94 |
| 9 | 0.50 | 0.015 | 1 | B2 | 5.89 | 30.0 | 2.94 |
| 10 | 0.50 | 0.000 | 0 | Nenhuma | 0.00 | 30.0 | 0.00 |
| 11 | 0.50 | 0.000 | 0 | Nenhuma | 0.00 | 30.0 | 0.00 |
| 12 | 0.50 | 0.000 | 0 | Nenhuma | 0.00 | 30.0 | 0.00 |
| 13 | 0.50 | 0.000 | 0 | Nenhuma | 0.00 | 30.0 | 0.00 |
| 14 | 0.50 | 0.000 | 0 | Nenhuma | 0.00 | 30.0 | 0.00 |
| 15 | 0.50 | 0.000 | 0 | Nenhuma | 0.00 | 30.0 | 0.00 |
| 16 | 0.50 | 0.000 | 0 | Nenhuma | 0.00 | 30.0 | 0.00 |
| 17 | 0.50 | 0.000 | 0 | Nenhuma | 0.00 | 30.0 | 0.00 |
| 18 | 1.20 | 0.000 | 0 | Nenhuma | 0.00 | 30.0 | 0.00 |
| 19 | 1.20 | 0.000 | 0 | Nenhuma | 0.00 | 30.0 | 0.00 |
| 20 | 1.20 | 0.000 | 0 | Nenhuma | 0.00 | 30.0 | 0.00 |
| 21 | 0.50 | 0.000 | 0 | Nenhuma | 0.00 | 30.0 | 0.00 |
| 22 | 0.50 | 0.000 | 0 | Nenhuma | 0.00 | 30.0 | 0.00 |
| 23 | 0.50 | 0.000 | 0 | Nenhuma | 0.00 | 30.0 | 0.00 |



### Resumo do Período
- **Horas de Operação:** 8 horas
- **Consumo Total de Energia:** 47,12 kWh
- **Volume Total Bombeado:** 432 m³
- **Custo Total Diário:** R$ 23,52





---

# 16. Robustez Numérica e Formulação DCP

<p align="justify">A implementação foi estruturada para obedecer às regras de Disciplined Convex Programming (DCP) do CVXPY. Embora o problema seja uma Programação Inteira Mista (MILP), toda a não linearidade hidráulica é pré-calculada antes da otimização. As perdas de carga, alturas manométricas e potências são calculadas para cada combinação de diâmetro e número de bombas, sendo armazenadas em matrizes constantes. Durante a otimização, o modelo manipula apenas constantes multiplicadas por variáveis binárias, preservando a linearidade da função objetivo e das restrições.</p>

<p align="justify">Essa estratégia evita produtos entre variáveis de decisão, divisões por variáveis e expressões quadráticas dentro do modelo de otimização, permitindo que o problema seja reconhecido como compatível com as regras DCP.</p>

<p align="justify">Outra medida importante consiste em representar as escolhas de engenharia por variáveis binárias e utilizar restrições de consistência para ativar apenas os parâmetros correspondentes ao diâmetro selecionado. Dessa forma, toda a lógica combinatória permanece linear.</p>

## 16.1 Como Evitar Soluções "optimal_inaccurate"

<p align="justify">Problemas classificados como <code>optimal_inaccurate</code> normalmente estão associados à tolerância numérica do solver e não necessariamente indicam que a solução seja inviável. Algumas práticas adotadas para reduzir esse comportamento são:</p>

<p align="justify">- pré-calcular todos os parâmetros hidráulicos antes da otimização;</p>
<p align="justify">- evitar coeficientes com escalas muito diferentes por meio de normalização quando necessário;</p>
<p align="justify">- utilizar apenas constantes nas expressões da função objetivo e das restrições;</p>
<p align="justify">- evitar produtos entre variáveis contínuas e binárias;</p>
<p align="justify">- preferir solvers MILP mais robustos, como CBC, HiGHS, SCIP ou GUROBI, quando disponíveis;</p>
<p align="justify">- verificar a condição <code>problema.is_dcp()</code> antes da resolução;</p>
<p align="justify">- analisar o status retornado pelo solver e, quando necessário, ajustar as tolerâncias numéricas.</p>

<p align="justify">Com essa formulação, o modelo permanece linear, atende às regras DCP do CVXPY e reduz significativamente a ocorrência de problemas de estabilidade numérica durante a otimização.</p>

---

# 17. Gráficos

<p align="center">
  <img src="https://github.com/rodfloripa/Projeto89/blob/main/fig2.png">
</p>


</p>
