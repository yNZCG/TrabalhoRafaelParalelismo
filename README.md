🗺️ Otimização de Rotas de Evacuação em Belo Horizonte via Programação Paralela


📌 Contexto do ProjetoContexto: Desenvolvido como parte da disciplina de Programação Paralela.Objetivo: Solucionar a computação de rotas de fuga e saídas em Belo Horizonte durante cenários de trânsito intenso ou emergências críticas.Abordagem: Paralelização de algoritmos de busca em grafos.

🗂️ O Problema e a Carga de Trabalho

 🏙️ Desafios UrbanosGargalos Viários: Severos pontos de retenção em grandes vias (ex: Anel Rodoviário, Av. do Contorno, Av. Cristiano Machado).Limitação Sequencial: O cálculo sequencial de caminhos mínimos a partir de múltiplos pontos congestionados é inviável em tempo real.
 
⚙️ Modelagem do Cenário de EstresseObjetivo da Simulação: Testar a escalabilidade do sistema em cenários extremos, englobando a capital e a Região Metropolitana.Vértices (200.000): Interseções, cruzamentos de vias e nós de tráfego de toda a malha viária expandida de forma proporcional.Arestas: Ruas e avenidas interconectadas com pesos baseados no tempo de deslocamento sob trânsito.Carga de Consulta (4.000 origens): Focos de retenção simultâneos calculando rotas de fuga concorrentemente para as saídas de BH.Fonte de Dados: Base de dados do Geofabrik.


🚀 Arquitetura e Estratégia de ParalelizaçãoEstratégia Adotada: Decomposição de Tarefas (Task Decomposition) no laço principal de busca.Classificação do Problema: Embarrassingly Parallel (Paralelismo Constrangedor), dado que a rota do ponto $A$ não interfere no cálculo do ponto $B$.Tecnologia Utilizada: Biblioteca OpenMP para gerenciamento das threads.


📊 Resultados ObtidosSerialTime
(1 Thread): 142.50 s | Speedup: 1.00x | Eficiência: 100.0%Paralelo 
(2 Threads): 72.10 s | Speedup: 1.97x | Eficiência: 98.5%Paralelo 
(4 Threads): 36.80 s | Speedup: 3.87x | Eficiência: 96.7%Paralelo 
(8 Threads): 19.20 s | Speedup: 7.42x | Eficiência: 92.7%
