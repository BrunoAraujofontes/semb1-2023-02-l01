# Questionário Sistemas Embarcados I

## 1. Explique brevemente o que é compilação cruzada (***cross-compiling***) e para que ela serve.
R: A compilacao cruzada é o processo de compilar um programa em um sistema diferente do executado e serve para codificar em sistemas com arquiteturas diferentes
como por exemplo nosso computador e o microcontrolador que possuem arquiteturas diferentes.
## 2. O que é um código de inicialização ou ***startup*** e qual sua finalidade?
R: é um conjunto de instrucoes que devem ocorrer quando o sistema é iniciado e sua finalidade é inicializar os stacks,inicializar  a secap .bss em zero, copiar o conteudo de
.data e .fast da memoria nao volatil para RAM, inicializar o heap , declarar a tabela de vetores de interrupcao e chamar a funcao main.
## 3. Sobre o utilitário **make** e o arquivo **Makefile responda**:

#### (a) Explique com suas palavras o que é e para que serve o **Makefile**.
R: O makefile é um arquivo que visa automatizar os processos de compilacao e sua finalidade é facilitar na manutencao do projeto,automatizar a compilacao,permitir a configuracao
de variaveis e opcoes de compilacao de forma centralizada e executa tarefas adicionais incluindo regras ou tarefas relacionadas ao desenvolvimento.
#### (b) Descreva brevemente o processo realizado pelo utilitário **make** para compilar um programa.
R: O utilitario make le as instrucoes e regras no arquivo makefile para entender como compilar o programa, verificando os arquivos fonte que foram modificados, executando comandos
de compilacao se necessario e assim utilizando os arquivos objeto para construir o programa.
#### (c) Qual é a sintaxe utilizada para criar um novo **target**?
R: Para criar um target a sintaxe é:
Target: prerequisites
        recipe
#### (d) Como são definidas as dependências de um **target**, para que elas são utilizadas?
R : As dependencias de um target sao definidas diretamente no arquivo makefine e sao utilizadas para listar os aquivos dos quais o target depende utilizando de pre-requisitos
essenciais na construcao do target.Pensando no codigo de sintaxe a seguir, prerequisites sao as dependencias.
Target: prerequisites
        recipe

#### (e) O que são as regras do **Makefile**, qual a diferença entre regras implícitas e explícitas?
R: As regras do Makefile sao instrucoes de geracao de um target que indicam os comandos que devem ser utilizados. A diferenca entre regras explicitas e implicitas sao que as regras 
explicitas sao especificacoes em relacao ao target com dependencias e instrucoes definidas diretamento pelo usuario, porem as regras implicitas utiliza de um meio automatico do cortex
que utiliza classes de arquivos com padroes de nomes semelhantes.
## 4. Sobre a arquitetura **ARM Cortex-M** responda:

### (a) Explique o conjunto de instruções ***Thumb*** e suas principais vantagens na arquitetura ARM. Como o conjunto de instruções ***Thumb*** opera em conjunto com o conjunto de instruções ARM?
R: O conjunto de instrucoes thumb é uma extensao do conjunto arm sendo reduzido e possuindo entao 16 bits.As vantagens da utilizacao do conjunto Thumb é o fato de ele possuir instrucoes mais compactas e,
portanto um codigo menor e mais otimizado e assim ocupando menos espaco na memoria. Para ambos os conjuntos operarrem juntos ocorre o chamado modo misto que é quando o processador executa instrucoes de ambos
no mesmo programa alternando entre cada um deles de acordo com a acao necessaria.
### (b) Explique as diferenças entre as arquiteturas ***ARM Load/Store*** e ***Register/Register***.
R: A diferenca entra essa arquiteturas é que a Load/Store restringe as operacoes de de carregamento e armazenamento de dados, load e store respectictamente, atraves de instrucoes especificas, porem
a register/memory permite que operacoes aritmeticas e logicas ocorram diretamente na memoria.
### (c) Os processadores **ARM Cortex-M** oferecem diversos recursos que podem ser explorados por sistemas baseados em **RTOS** (***Real Time Operating Systems***). Por exemplo, a separação da execução do código em níveis de acesso e diferentes modos de operação. Explique detalhadamente como funciona os níveis de acesso de execução de código e os modos de operação nos processadores **ARM Cortex-M**.
R: Existem 2 modos de operacao sendo eles handler mode e thread mode e tambem existem 2 niveis de acesso que sao o modo privilegiado e nao privilegiado.Assim, o funcionamento incia-se com o sistema em modo
thread mode que é o modo de execucao normal do codigo e nesse caso o modo privilegiado é o nivel de acesso nesse modo de operacao permitindo total acesso ao processador, porem ao ter uma interrupcao o sistema
troca o modo de operacao para handler mode que é o modo de tratamento de interrupcoes. Por fim, ao terminar de tratar das interrupcoes o sistema retorna para thread mode, porem com nivel de acesso nao privilegiado
que tem a funcao de restringir alguns acessos a recursos e areas da memoria.
### (d) Explique como os processadores ARM tratam as exceções e as interrupções. Quais são os diferentes tipos de exceção e como elas são priorizadas? Descreva a estratégia de **group priority** e **sub-priority** presente nesse processo.
R: Os processadores ARM tratam as excecoes e interrupcoes no modo handler mode, salvando o estado atual de execucao e ao fim do tratamento da excecao retorna ao modo
de execucao normal do codigo.Existem quatro tipos basicos de excecoes sendo elas as excecoes de hardware,software, externas e de sistemas e cada excecao recebe um
nivel de prioridade sendo executadas de acordo. Quando falamos sobre a priorizacao das excecoes no cortex-M temos a interrupcao reset que possui a maior prioridade,
em seguida temos o NMI, Hardfault e por fim as outras excecoes. A estrategia group priority e sub priority ocorre onde em group priority as excecoes sao agrupadas
de acordo com o nivel de prioridade, cujo cada grupo possui uma prioridade para ocorrer um controle da prioridade entre os grupos com interrupcoes mais importantes, ja
em sub priority dentro do grupo cada interrupcao tem uma subpropriedade para controle da prioridade entre interrupcoes de mesmo grupo.
### (e) Qual a diferença entre os registradores **CPSR** (***Current Program Status Register***) e **SPSR** (***Saved Program Status Register***)?
R: O registrador CPSR serve para armazenar informacoes sobre o atual estado do processador, condicoes de execucao, nivel de acesso e modo de operacao, ja o
SPSR tem a funcao de salvar o CPSR quando ocorre uma interrupcao.
### (f) Qual a finalidade do **LR** (***Link Register***)?
R: O LR tem a funcao de armazenar o endereco de memoria de retorna para apos a execucao de uma funcao ocorra o retorno para o ponto
de execucao do codigo anterior a chamada da funcao e assim seguindo o fluxo de execucao do codigo.
### (g) Qual o propósito do Program Status Register (PSR) nos processadores ARM?
R: O PSR é um registrador de informacoes sobre o estado de execucao do programa e seu proposito é controlar de maneira eficiente o estado do processador
na manipulacao de interrupcoes e execucao do codigo.
### (h) O que é a tabela de vetores de interrupção?
R: é uma tabela de vetores que tratam de eventos de varios tipos realizando possiveis interrupcoes para controle de eventos no sistema.
### (i) Qual a finalidade do NVIC (**Nested Vectored Interrupt Controller**) nos microcontroladores ARM e como ele pode ser utilizado em aplicações de tempo real?
R: A finalidade do NVIC é facilitar o tratamento de interrupcoes permitindo, por exemplo a definicao de prioridade de cada interrupcao e realizando o gerenciamento
de interrupcoes aninhadas e portanto, sendo utilizadas em inumeras aplicacoes de tempo real por exemplo, realizar o tratamento de interrupcoes cruciais de maneira
mais rapida com o uso de prioridae citado anteriormente.
### (j) Em modo de execução normal, o Cortex-M pode fazer uma chamada de função usando a instrução **BL**, que muda o **PC** para o endereço de destino e salva o ponto de execução atual no registador **LR**. Ao final da função, é possível recuperar esse contexto usando uma instrução **BX LR**, por exemplo, que atualiza o **PC** para o ponto anterior. No entanto, quando acontece uma interrupção, o **LR** é preenchido com um valor completamente  diferente,  chamado  de  **EXC_RETURN**.  Explique  o  funcionamento  desse  mecanismo  e especifique como o **Cortex-M** consegue fazer o retorno da interrupção. 
R: Quando a funcao é chamada por BL o endereco de retorno é armazenado no LR, porem caso ocorra uma interrupcao o cortex-m automaticamente salva o contexto da execucao atual preenchendo LR
com o Valor EXC_RETURN, assim quando a instrucao BX LR ocorrer, o retorno da interrupcao ocorrera restaurando o contexto anterior a interrupcao.
### (k) Qual  a  diferença  no  salvamento  de  contexto,  durante  a  chegada  de  uma  interrupção,  entre  os processadores Cortex-M3 e Cortex M4F (com ponto flutuante)? Descreva em termos de tempo e também de uso da pilha. Explique também o que é ***lazy stack*** e como ele é configurado. 
R:A diferenca entre eles é que o cortex-M3 empilha manualmente os registradores de r0 a r15, porem o o cortex M4F adiciona registradores de ponto flutuante a cada contexto que precisa ser salvo
e por isso, em termos de tempo e uso de pilha nota-se que o M4F utiliza mais espaco da pilha alem de demandar mais tempo para realizacao do salvamento do contexto. Desse modo, o Lazy stack é uma
solucao para este problema de desempenho ja que tem a funcao de salvar somente os contextos que sejam realmente necessarios no tratamento da interrupcao.

## Referências

### Básicas

[1] [STM32F411xC Datasheet](https://www.st.com/resource/en/datasheet/stm32f411ce.pdf)

[2] [RM0383 Reference Manual](https://www.st.com/resource/en/reference_manual/rm0383-stm32f411xce-advanced-armbased-32bit-mcus-stmicroelectronics.pdf)

[3] [Using the GNU Compiler Collection (GCC)](https://gcc.gnu.org/onlinedocs/gcc/index.html)

[4] [GNU Make](https://www.gnu.org/software/make/manual/html_node/index.html)

### Vídeos Microsoft Teams

[5] [05 - Introdução à arquitetura de computadores](https://web.microsoftstream.com/embed/channel/f6b3a0de-e6f3-4652-b2d5-f1164032498a?app=microsoftteams&sort=undefined&l=pt-br#)

[6] [06 - Arquitetura Cortex-M Parte 1/2](https://web.microsoftstream.com/embed/channel/f6b3a0de-e6f3-4652-b2d5-f1164032498a?app=microsoftteams&sort=undefined&l=pt-br#)

[7] [07 - Arquitetura Cortex-M Parte 2/2](https://web.microsoftstream.com/embed/channel/f6b3a0de-e6f3-4652-b2d5-f1164032498a?app=microsoftteams&sort=undefined&l=pt-br#)

[8] [08 - Microcontroladores STM32](https://web.microsoftstream.com/embed/channel/f6b3a0de-e6f3-4652-b2d5-f1164032498a?app=microsoftteams&sort=undefined&l=pt-br#)

[9] [10 - Introdução à arquitetura de computadores](https://web.microsoftstream.com/embed/channel/f6b3a0de-e6f3-4652-b2d5-f1164032498a?app=microsoftteams&sort=undefined&l=pt-br#)

### Material Suplementar

[5] [A General Overview of What Happens Before main()](https://embeddedartistry.com/blog/2019/04/08/a-general-overview-of-what-happens-before-main/)
 
[6] [Bare metal embedded lecture-1: Build process](https://youtu.be/qWqlkCLmZoE?si=mn5yDnJYudQ1PpZH)
 
[7] [Bare metal embedded lecture-2: Makefile and analyzing relocatable obj file](https://youtu.be/Bsq6P1B8JqI?si=yuNLPj3JQ-2IT1yo)
 
[8] [Bare metal embedded lecture-3: Writing MCU startup file from scratch](https://youtu.be/2Hm8eEHsgls?si=c27MpZ47ApiMSwHR)
 
[9] [Lecture 15: Booting Process](https://youtu.be/3brOzLJmeek?si=MsHRUEJP8zofjwJQ)
