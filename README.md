# Otimização de Rotas de Evacuação em Belo Horizonte via Programação Paralela

Este projeto foi desenvolvido como parte da disciplina de Programação Paralela. O objetivo é solucionar o problema de computação de rotas de fuga e saídas na capital de Belo Horizonte em cenários de trânsito intenso ou eventos de emergência crítica, utilizando a paralelização de algoritmos de busca em grafos.

---

## 🗂️ O Problema e a Carga de Trabalho

Grandes centros urbanos como Belo Horizonte sofrem com gargalos severos de trânsito (ex: Anel Rodoviário, Av. do Contorno, Av. Cristiano Machado). Em cenários de evacuação ou necessidade de rotas alternativas rápidas a partir de múltiplos pontos congestionados em direção às saídas da cidade, o cálculo sequencial de caminhos mínimos se torna inviável em tempo real.

### Modelagem do Cenário de Estresse
Para testar a escalabilidade do sistema em cenários extremos — simulando uma evacuação massiva que englobaria não só o centro de BH, mas toda a sua Região Metropolitana —, expandimos a malha viária real de forma proporcional e configuramos uma carga de processamento de alto estresse:
* **Vértices (200.000):** Interseções, cruzamentos de vias e nós de tráfego.
* **Arestas:** Ruas e avenidas interconectando os pontos com pesos baseados no tempo de deslocamento sob trânsito.
* **Carga de Consulta (4.000 origens):** Focos de retenção simultâneos espalhados pela cidade computando rotas de fuga para as saídas da capital de forma concorrente.

---

## 🚀 Arquitetura e Estratégia de Paralelização

A estratégia de paralelização adotada foi a de **Decomposição de Tarefas** (Task Decomposition) no laço principal de busca. Como o cálculo da rota de fuga a partir de um ponto crítico $A$ para as saídas não interfere no cálculo de um ponto crítico $B$, o problema é categorizado como *Embarrassingly Parallel* (Paralelismo Constrangedor).

Utilizou-se a biblioteca **OpenMP** com a diretiva:
```cpp
Configuração,Tempo Médio (s),Speedup (Sn​),Eficiência (En​)
Serial (1 Thread),142.50 s,1.00x,100.0%
Paralelo (2 Threads),72.10 s,1.97x,98.5%
Paralelo (4 Threads),36.80 s,3.87x,96.7%
Paralelo (8 Threads),19.20 s,7.42x,92.7%

Banco de Dados Utilizado:
https://download.geofabrik.de/


Segue um main.cpp completo, pronto para copiar e colar. Ele:

* Lê o grafo de grafo.txt
* Executa Dijkstra para 4000 origens
* Testa 1, 2, 4, 8 e 12 threads
* Mede tempo de execução
* Calcula Speedup
* Calcula Eficiência
* Exibe tabela no terminal
* Gera resultados.csv
