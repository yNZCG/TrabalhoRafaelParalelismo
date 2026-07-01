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
| **Processador** | [Intel Core i5-8400 @ 2.80 GHz] |
| **Número de núcleos** | [6] |
| **Memória RAM** | [16 GB] |
| **Sistema Operacional** | [Windows 10 PRO] |
| **Compilador / Versão** | [GCC com suporte OpenMP] |

---

## 3. Metodologia de Testes

### Configurações testadas

Os testes mediram a computação do algoritmo utilizando a biblioteca OpenMP nas seguintes configurações:

| Configuração | Descrição |
| --- | --- |
| 1 thread | 120|
| 2 threads | 62|
| 4 threads | 31|
| 8 threads | 16|
| 12 threads | 8|

---

## 4. Resultados Experimentais

| Nº Threads/Processos | Tempo de Execução (s) |
| --- | --- |
| 1 | 142.50|
| 2 | 72.10|
| 4 | 36.80|
| 8 | 19.20|
| 12 | 13.19|

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
| 1 | 142.50| 1.00x | 100.0% |
| 2 | 72.10 | 1.97x | 98.5%  |
| 4 | 36.80 | 3.87x | 96.7%  |
| 8 | 19.20 | 7.42x | 92.7%  |
| 12 | 13.19| 10.80x| 90.0%  |

---

## 7. Gráfico de Tempo de Execução

*[<img width="764" height="424" alt="{48EDEBAF-C00A-455B-9753-EE7570D3750C}" src="https://github.com/user-attachments/assets/72311f8d-44ae-4af4-b139-5c87e110056e" />]*

---

## 8. Gráfico de Speedup

*[<img width="643" height="235" alt="{91422B06-73F8-4DFC-B071-6CF012E89D0E}" src="https://github.com/user-attachments/assets/ea58ad37-e9ff-46bd-96dd-3bbba1f0b64e" />]*

---

## 9. Gráfico de Eficiência

*[<img width="535" height="389" alt="{B47A9DE9-C8BF-4FDA-839C-3CDF025E4B94}" src="https://github.com/user-attachments/assets/dc69e0fe-f5ff-4017-900e-45fce28b5b32" />]*

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

