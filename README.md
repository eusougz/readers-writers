# Readers&Writers
## Syncronization Proccess
### Lab. Sistemas Operacionais
### Members: Guilherme Giacomin e Uriel Braga

#### How to compile:

`$ gcc readers_writers.c -lpthread && ./a.out 50 10 10`

#### Explanation (in portuguese):

No comando de execução, existem três parâmetros após o `./a.out`:
O primeiro se refere ao tempo de execução da main().
O segundo indica o número de threads escritores.
O terceiro, e último, informa o número de threads leitores.

O algoritmo **semáforo**, que consiste na execução de até N threads simultaneamente por meio de um counter (no código é chamado de *empty*) que possui o mesmo valor de N e, a cada interação, sofre um aumento ou uma diminuição, a fim de indicar quantas threads podem ser executadas, é capaz de permitir a sincronização de processos. 
No projeto, foi feito um teste desse algoritmo por meio da manipulação de uma variável compartilhada a todas threads (*shared_data*). O valor de N utilizado é igual a 3, ou seja, 3 leitores podem acessar simultaneamente a seção crítica (que contém a leitura do dado compartilhado) de seus respectivos processos. 
Quando um escritor está prestes a executar, o mesmo bloqueia todos escritores utilizando espera ocupada com os comandos **TSL** (*__sync_lock_test_and_set* e *__sync_lock_release*), a fim de evitar inconsistências na variável compartilhada. A ideia consiste em, enquanto a variável *writer_lock*, manipulada pelos comandos citados anteriormente, indicar que um processo está bloqueado, isto é, ter valor igual a 1, nenhum outro processo terá acesso a sua respectiva região crítica.
