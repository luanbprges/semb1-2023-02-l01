# Questionário Sistemas Embarcados I - Luan Cardoso Borges

## 1. Explique brevemente o que é compilação cruzada (***cross-compiling***) e para que ela serve.
O Cross-Compiling se trata de uma compilação entre arquiteturas diferentes, ou seja, é um processo onde é possível compilar um arquivo atráves de um computador com uma arquitetura, gerando um outro arquivo que consiga ser lido por um dispositivo diferente e com uma outra arquitetura.


## 2. O que é um código de inicialização ou ***startup*** e qual sua finalidade?
Um código de inicialização, ou como é conhecido, startup, é um código criado para executar algumas tarefas que antecedem a execução da função principal (main) em um programa. Como por exemplo: a inicialização do stack, copiar conteúdo de uma seção para outra, inicializar variavies globais, inicializar a seção .bss em zero, entre outras atividades essenciais que garantem o funcionamento do programa.


## 3. Sobre o utilitário **make** e o arquivo **Makefile responda**:

#### (a) Explique com suas palavras o que é e para que serve o **Makefile**.
O Makefile é um arquivo onde contém instruções que serão executadas pelo make, nele é possivel escrever regras para compilar um arquivo de forma automática, sem correr o risco de cometer erros ao fazer esse processo de forma manual. Essas regras especificam como os diferentes componentes de um projeto devem ser compilados e vinculados, permitindo uma compilação e um processo de construção do software mais eficiente e livre de erros.


#### (b) Descreva brevemente o processo realizado pelo utilitário **make** para compilar um programa.
O processo de compilaçõa se inicia com o make fazendo a leitura do arquivo Makefile, examinando as regras presentes nele, ou seja, avalia se os targets estão desatualizados através das suas dependências (prerequisites). Um target é dado como desatualizado caso não exista ou sua data de modificação seja mais antiga que seus prerequisitos, entendendo assim que precisa ser atualizado. 
A forma como os targets são atualizados é definido pelas recipes de cada um, essas receitas contêm os comandos necessários para compilar, montar ou construir o target específico, utilizando as informações disponíveis nos prerequisitos.


#### (c) Qual é a sintaxe utilizada para criar um novo **target**?
Para criar um novo target deve-se obedecer o seguinte formato:

targets: prerequisites
	recipe 

Onde "targets" é o nome do novo target; prerequisites são os arquivos ou outros targets que o target atual depende, se esses pre requisitos não estiverem atualizados, o target será reconstruído; e recipe são os comandos que o make deve executar para criar o target, eles devem começar por uma tabulação. 


#### (d) Como são definidas as dependências de um **target**, para que elas são utilizadas?
As dependências de um target são definidas para indicar os arquivos necessários para compilar ou executar o target em questão. Se alguma dependência não estiver presente ou desatualizada, o make pode tentar compilá-la automaticamente ou gerar um erro indicando que a dependência está faltando ou desatualizada. Se todas as dependências estiverem disponíveis e atualizadas, o target pode ser compilado ou executado com sucesso.


#### (e) O que são as regras do **Makefile**, qual a diferença entre regras implícitas e explícitas?
As regras em um Makefile são instruções que especificam como transformar um ou mais arquivos de uma origem em um arquivo específico desejado, elas são compostas pelos targets, prerequisites e recipes. 
A diferença entre regra explícita e implícita, é que na primeira os arquivos escolhidos para serem compilados são definidos pela extensão do arquivo (Exemplo: Todos arqivos .c), já na regra implícita os arquivos são escolhidos pelos seus nomes que pode ser definido pelo usuário (Exemplo: main.c).  


## 4. Sobre a arquitetura **ARM Cortex-M** responda:

### (a) Explique o conjunto de instruções ***Thumb*** e suas principais vantagens na arquitetura ARM. Como o conjunto de instruções ***Thumb*** opera em conjunto com o conjunto de instruções ARM?
As instruções thumb são um conjunto de instruções desenvolvidas pela ARM com o objetivo de melhorar a eficiência da codificação de um código. Com essa finalidade, as intruções thumb foram projetadas em 16 bits, diferentemente das instruções ARM convencionais de 32 bits. Portanto, devido elas serem codificadas em 16 bits, resulta-se em um código menor ou é possivel até mesmo escrever mais instruções na mesma quantidade de memória em comparação com instruções ARM convencionais.
O conjunto de instruções Thumb opera em conjunto com o conjunto de instruções ARM em um sistema ARM através de um modo de operação chamado "modo Thumb". Nesse modo, o processador executa instruções Thumb em vez de instruções ARM convencionais, essa transição pode ser realizada por meio de instruções de salto especiais que alteram o estado do processador.


### (b) Explique as diferenças entre as arquiteturas ***ARM Load/Store*** e ***Register/Memory***.
Na arquitetura ARM Load/Store, as operações de leitura (load) e escrita (store) na memória são realizadas exclusivamente por instruções dedicadas, como LDR (Load Register) e STR (Store Register). Isso significa que para manipular dados na memória, é necessário carregar primeiro os valores desejados em registradores e, em seguida, executar operações de carga ou armazenamento. As operações aritméticas e lógicas são realizadas somente entre registros, sem acesso direto à memória.
Já na arquitetura Register/Memory, as instruções aritméticas e lógicas podem acessar diretamente a memória para operações de leitura e escrita, sem a necessidade de instruções de carga e armazenamento separadas. Isso permite que as operações sejam realizadas de forma mais integrada e eficiente, já que os dados podem ser acessados diretamente na memória, sem a necessidade de transferências adicionais entre registradores e memória.


### (c) Os processadores **ARM Cortex-M** oferecem diversos recursos que podem ser explorados por sistemas baseados em **RTOS** (***Real Time Operating Systems***). Por exemplo, a separação da execução do código em níveis de acesso e diferentes modos de operação. Explique detalhadamente como funciona os níveis de acesso de execução de código e os modos de operação nos processadores **ARM Cortex-M**.
Os níveis de acesso de execução de código são divididos em: Privilegiado (Privileged) e Não-privilegiado (Unprivileged). Onde no primeiro, o código tem acesso total aos recursos do processador e do sistema, sendo assm, ele pode acessar todas as instruções do processador e operar em qualquer área da memória. Já no unprivileged, o código neste nível tem acesso restrito aos recursos do sistema.
Os modos de operação são dividos em quatro: Handler Mode, Thread Mode, Privileged Mode e User Mode. O Handler Mode é ativado em resposta a uma interrupção ou exceção, é durante esse modo que é lidado com a interrupção ou exceção; O Thread Mode é o modo padrão de execução do código do aplicativo, quando nenhum evento de exceção ou interrupção está ocorrendo, o processador opera no modo de thread; O Privileged Mode é o modo que permite que o código execute instruções privilegiadas e acesse recursos do sistema que não estão disponíveis no modo não-privilegiado; O User Mode é o modo de operação de código não-privilegiado, onde o código tem acesso limitado aos recursos do sistema.


### (d) Explique como os processadores ARM tratam as exceções e as interrupções. Quais são os diferentes tipos de exceção e como elas são priorizadas? Descreva a estratégia de **group priority** e **sub-priority** presente nesse processo.
Quando uma exceção ou uma interrupção é gerada, o processador suspende a execução normal do progama e salva o estado atual do processador no stack. Em seguida, o controle do processador é passado para um tratador específico dessa exceção/interrupção cujo endereço está armazenado em uma tabela de vetores de exceção/interrupção, após tratar a causa desse problema, é restaurado o estado do processador e a execução do programa principal é retomada.
Os diferentes tipos de exceções são: Exceção Sincrona e Exceção Assincrona. As exceções sincronas são causadas por instruções que estão sendo executadas e as assincronas são geradas por causas externas ao processador e não possuem relaçao com a instrução que está sendo executada. Essas exceções e interrupções são priorizadas de acordo com sua importância, o ARM utiliza um esquema de prioridade onde números mais baixos indicam interrupções mais prioritárias.
Nos processadores ARM, o conceito de Group Priority e Sub-Priority é fundamental para organizar e priorizar exceções e interrupções de maneira eficiente. Imagine que o processador possui diferentes conjuntos de exceções e interrupções que podem ocorrer durante a execução do programa. Para lidar com elas de forma ordenada, são estabelecidos grupos de prioridade, cada um com sua própria prioridade global. Esses grupos podem representar diferentes níveis de urgência, onde eventos críticos têm prioridade sobre os menos críticos. Dentro de cada grupo de prioridade, as exceções e interrupções podem ser ainda mais diferenciadas por meio de subprioridades, isso permite uma classificação mais refinada dos eventos dentro do mesmo grupo. Por exemplo, se várias interrupções de um grupo de prioridade média ocorrerem simultaneamente, a subprioridade pode ser utilizada para determinar a ordem de tratamento, priorizando aquela que é mais crítica ou relevante naquele momento.


### (e) Qual a diferença entre os registradores **CPSR** (***Current Program Status Register***) e **SPSR** (***Saved Program Status Register***)?
Tanto o CPSR quanto o SPSR são utilizados nos processadore ARM para armazenar informações sobre o estado do processador, porém o CPSR armazena informações sobre o estado atual do processador durante a execução de um programa, como flags de condição (como zero, negativo, carry e overflow), o modo de operação atual do processador (como modo de usuário, modo privilegiado, modo IRQ e modo FIQ) e o estado de interrupção (indicando se as interrupções estão habilitadas ou desabilitadas), além disso, o CPSR é frequentemente utilizado para controlar a execução do programa e determinar como o processador deve responder a eventos como exceções e interrupções. 
Já os registradores SPSR armazena temporariamente o estado do processador quando uma exceção ocorre. Ou seja, durante a execução normal do programa, o SPSR permanece inalterado e não é acessado diretamente pelo programa, portanto, quando uma exceção ocorre, o CPSR é copiado para o SPSR para preservar o estado anterior do processador. Isso permite que o processador retorne ao estado original após o tratamento da exceção, restaurando o CPSR a partir do valor armazenado no SPSR.


### (f) Qual a finalidade do **LR** (***Link Register***)?
O Link Register (LR) possui a finalidade de armazenar o endereço de retorno de uma subrotina, ou seja, ao finalizar uma subrotina o programa consegue recuperar o endereço em que estava executando através do valor armazenado no link register.



### (g) Qual o propósito do Program Status Register (PSR) nos processadores ARM?
O Program Status Register possui a finalidade de armazenar as informações sobre o estado de operação atual do processador, além de controlar a ativação e desativação das interrupções e definir o modo de operação do processador.


### (h) O que é a tabela de vetores de interrupção?
A tabela de vetores de interrupção em uma arquitetura ARM Cortex-M é uma tabela que mapeia as diferentes fontes de interrupção para os respectivos tratadores de interrupção, ou seja, cada entrada na tabela representa uma fonte de interrupção específica e contém o endereço de memória do tratador de interrupção associado a essa fonte de interrupção.
Quando ocorre uma interrupção, o processador ARM Cortex-M usa o número da interrupção como um índice para acessar a entrada correspondente na tabela de vetores de interrupção. Ele então obtém o endereço de memória do tratador de interrupção a partir dessa entrada e transfere o controle para esse endereço, executando o código do tratador de interrupção.


### (i) Qual a finalidade do NVIC (**Nested Vectored Interrupt Controller**) nos microcontroladores ARM e como ele pode ser utilizado em aplicações de tempo real?
Todas estas interrupções são configuradas por meio de um periférico conhecido como NVIC (Nested Vectored Interrupt Controller), cuja finalidade principal é coordenar e priorizar as interrupções que ocorrem no sistema. Ou seja, o NVIC ajuda a garantir que as interrupções sejam tratadas na ordem certa e no momento certo, para que o sistema possa reagir rapidamente a eventos importantes, sem perder o ritmo. 


### (j) Em modo de execução normal, o Cortex-M pode fazer uma chamada de função usando a instrução **BL**, que muda o **PC** para o endereço de destino e salva o ponto de execução atual no registador **LR**. Ao final da função, é possível recuperar esse contexto usando uma instrução **BX LR**, por exemplo, que atualiza o **PC** para o ponto anterior. No entanto, quando acontece uma interrupção, o **LR** é preenchido com um valor completamente  diferente,  chamado  de  **EXC_RETURN**.  Explique  o  funcionamento  desse  mecanismo  e especifique como o **Cortex-M** consegue fazer o retorno da interrupção. 
Normalmente, quando uma função é chamada usando a instrução BL, o endereço de retorno é salvo no LR, permitindo que o programa retorne ao ponto de chamada após a conclusão da função. No entanto, quando uma interrupção ocorre, o Cortex-M preenche o registro LR com um valor especial chamado EXC_RETURN, esse valor é uma instrução específica que indica ao processador como retornar de uma exceção. O valor EXC_RETURN contém informações sobre o contexto anterior da pilha, incluindo o modo de exceção original e o estado dos registradores salvos durante a entrada na exceção. Isso permite que o processador restaure o contexto exato em que estava antes da interrupção.


### (k) Qual  a  diferença  no  salvamento  de  contexto,  durante  a  chegada  de  uma  interrupção,  entre  os processadores Cortex-M3 e Cortex M4F (com ponto flutuante)? Descreva em termos de tempo e também de uso da pilha. Explique também o que é ***lazy stack*** e como ele é configurado. 
No Cortex M4F, que suporta operações de ponto flutuante, é necessário salvar registros específicos e status adicionais no stack durante interrupções ou exceções, além do contexto geral do processador, como outros registradores e o Link Register. Por outro lado, o Cortex M3 não suporta operações de ponto flutuante, portanto, apenas o contexto tradicional é preservado. O processo de salvamento do contexto no Cortex M4F requer mais tempo e uso de memória do stack em comparação com o Cortex M3, devido à inclusão dos registros específicos para ponto flutuante. 
No entanto, o Lazy Stack é uma configuração que otimiza esse processo. Quando ativado, o Lazy Stack permite que o contexto de ponto flutuante seja salvo no stack apenas se a interrupção ou exceção em questão realmente utilizar valores de ponto flutuante. O Lazy Stack é configurado através do registrador FPCCR, onde a ativação é indicada pelos bits 31 (ASPEN) e 30 (LSPEN) ambos definidos como 1. 





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