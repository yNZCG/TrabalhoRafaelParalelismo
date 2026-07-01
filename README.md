Aqui está a estrutura do seu projeto adaptada para o modelo que você enviou. Os campos que não constavam no seu texto original foram deixados com marcadores `[Preencher]` para que você possa completar posteriormente.

# Relatório — Otimização de Rotas de Evacuação em Belo Horizonte via Programação Paralela



| Campo | Informacao |
| --- | --- |
| **Disciplina** | Programação Paralela

 |
| **Aluno(s)** | Samuel de Souza |
| **Turma** | [Preencher] |
| **Professor** | [Preencher] |

---

## Sumário[cite: 1]

1. [Descrição do Problema](https://www.google.com/search?q=%231-descri%C3%A7%C3%A3o-do-problema)
2. [Ambiente Experimental](https://www.google.com/search?q=%232-ambiente-experimental)
3. [Metodologia de Testes](https://www.google.com/search?q=%233-metodologia-de-testes)
4. [Resultados Experimentais](https://www.google.com/search?q=%234-resultados-experimentais)
5. [Cálculo de Speedup e Eficiência](https://www.google.com/search?q=%235-c%C3%A1lculo-de-speedup-e-efici%C3%AAncia)
6. [Tabela de Resultados](https://www.google.com/search?q=%236-tabela-de-resultados)
7. [Gráfico de Tempo de Execução](https://www.google.com/search?q=%237-gr%C3%A1fico-de-tempo-de-execu%C3%A7%C3%A3o)
8. [Gráfico de Speedup](https://www.google.com/search?q=%238-gr%C3%A1fico-de-speedup)
9. [Gráfico de Eficiência](https://www.google.com/search?q=%239-gr%C3%A1fico-de-efici%C3%AAncia)
10. [Análise dos Resultados](https://www.google.com/search?q=%2310-an%C3%A1lise-dos-resultados)
11. [Conclusão](https://www.google.com/search?q=%2311-conclus%C3%A3o)
12. [Referências](https://www.google.com/search?q=%2312-refer%C3%AAncias)

---

## 1. Descrição do Problema

### Contexto e Relevância

A capital e a Região Metropolitana enfrentam severos pontos de retenção em grandes vias, como o Anel Rodoviário, a Av. do Contorno e a Av. Cristiano Machado. O cálculo sequencial de caminhos mínimos a partir de múltiplos pontos congestionados é inviável em tempo real. Este projeto foi desenvolvido para solucionar a computação de rotas de fuga e saídas em Belo Horizonte durante cenários de trânsito intenso ou emergências críticas.

### Qual é o objetivo do programa?

O objetivo principal da simulação é testar a escalabilidade do sistema em cenários extremos, englobando a capital e a Região Metropolitana.

### Qual o volume de dados processado?

A modelagem do cenário de estresse utilizou dados extraídos da base de dados do Geofabrik, contemplando:

* **Vértices (200.000):** Representam interseções, cruzamentos de vias e nós de tráfego de toda a malha viária expandida de forma proporcional.


* **Arestas:** Correspondem às ruas e avenidas interconectadas, com pesos baseados no tempo de deslocamento sob trânsito.


* **Carga de Consulta (4.000 origens):** Simula focos de retenção simultâneos, calculando rotas de fuga concorrentemente para as saídas de Belo Horizonte.



### Qual algoritmo foi utilizado?

Foi empregada a paralelização de algoritmos de busca em grafos. A estratégia de arquitetura adotada baseou-se na Decomposição de Tarefas (Task Decomposition) focada no laço principal de busca. O gerenciamento das threads foi realizado utilizando a Biblioteca OpenMP.

### Qual a complexidade aproximada do problema?

O problema foi classificado como *Embarrassingly Parallel* (Paralelismo Constrangedor). Essa classificação se dá pelo fato de que o cálculo da rota partindo de um ponto A não interfere no cálculo da rota partindo de um ponto B.

---

## 2. Ambiente Experimental

> **Nota:** *Informações de hardware não detalhadas no arquivo original. Preencha os dados da máquina utilizada para rodar os testes do OpenMP.*

| Item | Descrição |
| --- | --- |
| **Processador** | [Preencher - Ex: Intel Core i7] |
| **Número de núcleos** | [Preencher] |
| **Memória RAM** | [Preencher] |
| **Sistema Operacional** | [Preencher] |
| **Compilador / Versão** | [Preencher - Ex: GCC com suporte OpenMP] |

---

## 3. Metodologia de Testes

### Configurações testadas

Os testes mediram a computação do algoritmo utilizando a biblioteca OpenMP nas seguintes configurações:

| Configuração | Descrição |
| --- | --- |
| 1 thread | Versão Serial — baseline de comparação

 |
| 2 threads | Versão Paralela

 |
| 4 threads | Versão Paralela

 |
| 8 threads | Versão Paralela

 |
| 12 threads | Versão Paralela

 |

---

## 4. Resultados Experimentais

| Nº Threads/Processos | Tempo de Execução (s) |
| --- | --- |
| 1 | 142.50

 |
| 2 | 72.10

 |
| 4 | 36.80

 |
| 8 | 19.20

 |
| 12 | 13.19

 |

---

## 5. Cálculo de Speedup e Eficiência[cite: 1]

### Speedup[cite: 1]

$$Speedup(p) = \frac{T(1)}{T(p)}$$

[cite: 1]

onde:[cite: 1]

* $T(1)$ = tempo da execução serial[cite: 1]
* $T(p)$ = tempo com $p$ threads/processos[cite: 1]

### Eficiência[cite: 1]

$$Eficiência(p) = \frac{Speedup(p)}{p}$$

[cite: 1]

onde:[cite: 1]

* $p$ = número de threads ou processos[cite: 1]

---

## 6. Tabela de Resultados

| Threads (p) | Tempo (s) | Speedup S(p) | Eficiência E(p) |
| --- | --- | --- | --- |
| 1 | 142.50

 | 1.00x

 | 100.0%

 |
| 2 | 72.10

 | 1.97x

 | 98.5%

 |
| 4 | 36.80

 | 3.87x

 | 96.7%

 |
| 8 | 19.20

 | 7.42x

 | 92.7%

 |
| 12 | 13.19

 | 10.80x

 | 90.0%

 |

---

## 7. Gráfico de Tempo de Execução

*[Inserir aqui o Gráfico de Tempo de Execução comparando as threads]*

---

## 8. Gráfico de Speedup

*[Inserir aqui o Gráfico de Speedup × Threads]*

---

## 9. Gráfico de Eficiência

*[Inserir aqui o Gráfico de Eficiência (%) × Threads]*

---

## 10. Análise dos Resultados

Os resultados obtidos demonstram que a paralelização com OpenMP proporcionou ganhos substanciais de desempenho. O tempo de execução da versão serial foi de 142.50 segundos. Ao adotar 12 threads, o tempo reduziu significativamente para 13.19 segundos.

A aplicação apresentou excelente escalabilidade, resultando em um Speedup de 10.80x utilizando 12 threads. A eficiência manteve-se consistentemente alta em todos os cenários testados, decaindo de maneira muito leve e alcançando 90.0% na configuração de paralelismo máximo. Esse comportamento altamente eficiente confirma a característica do problema de ser *Embarrassingly Parallel*, onde a ausência de dependências diretas entre os cálculos das rotas evita grandes gargalos de sincronização.

---

## 11. Conclusão

A aplicação da decomposição de tarefas para o algoritmo de busca em grafos provou ser uma estratégia altamente eficiente para a resolução do gargalo de evacuação urbana. O modelo conseguiu absorver a carga de 4.000 pontos de origem simultâneos em uma malha viária de 200.000 vértices de maneira viável. A alta eficiência (nunca inferior a 90.0%) ressalta que o sistema escalou com sucesso em cenários extremos, comprovando que a estratégia adotada é capaz de processar as rotas de fuga com a agilidade necessária para o mundo real.

---

## 12. Referências

* Base de dados cartográficos extraída do Geofabrik.


* [Adicionar eventuais literaturas e referências extras utilizadas na modelagem e na biblioteca OpenMP]
