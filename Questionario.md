# Questionário Sistemas Embarcados I

## 1. Explique brevemente o que é compilação cruzada (***cross-compiling***) e para que ela serve.
O Cross-Compiling se trata de uma compilação entre arquiteturas diferentes, ou seja, através dele é possível compilar um arquivo atráves de um computador com uma arquitetura, gerando um outro arquivo que consiga ser lido por um dispositivo diferente e com uma outra arquitetura.


## 2. O que é um código de inicialização ou ***startup*** e qual sua finalidade?
Um código de inicialização, ou como é conhecido, startup, é um código criado para executar algumas tarefas que antecedem a execução da função principal (main) em um programa. Como por exemplo: copiar conteúdo de uma seção para outra, inicializar variavies globais, inicializar a seção .bss em zero, entre outras atividades essenciais que garantem o funcionamento do programa.


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

### (b) Explique as diferenças entre as arquiteturas ***ARM Load/Store*** e ***Register/Register***.

### (c) Os processadores **ARM Cortex-M** oferecem diversos recursos que podem ser explorados por sistemas baseados em **RTOS** (***Real Time Operating Systems***). Por exemplo, a separação da execução do código em níveis de acesso e diferentes modos de operação. Explique detalhadamente como funciona os níveis de acesso de execução de código e os modos de operação nos processadores **ARM Cortex-M**.

### (d) Explique como os processadores ARM tratam as exceções e as interrupções. Quais são os diferentes tipos de exceção e como elas são priorizadas? Descreva a estratégia de **group priority** e **sub-priority** presente nesse processo.

### (e) Qual a diferença entre os registradores **CPSR** (***Current Program Status Register***) e **SPSR** (***Saved Program Status Register***)?

### (f) Qual a finalidade do **LR** (***Link Register***)?

### (g) Qual o propósito do Program Status Register (PSR) nos processadores ARM?

### (h) O que é a tabela de vetores de interrupção?

### (i) Qual a finalidade do NVIC (**Nested Vectored Interrupt Controller**) nos microcontroladores ARM e como ele pode ser utilizado em aplicações de tempo real?

### (j) Em modo de execução normal, o Cortex-M pode fazer uma chamada de função usando a instrução **BL**, que muda o **PC** para o endereço de destino e salva o ponto de execução atual no registador **LR**. Ao final da função, é possível recuperar esse contexto usando uma instrução **BX LR**, por exemplo, que atualiza o **PC** para o ponto anterior. No entanto, quando acontece uma interrupção, o **LR** é preenchido com um valor completamente  diferente,  chamado  de  **EXC_RETURN**.  Explique  o  funcionamento  desse  mecanismo  e especifique como o **Cortex-M** consegue fazer o retorno da interrupção. 

### (k) Qual  a  diferença  no  salvamento  de  contexto,  durante  a  chegada  de  uma  interrupção,  entre  os processadores Cortex-M3 e Cortex M4F (com ponto flutuante)? Descreva em termos de tempo e também de uso da pilha. Explique também o que é ***lazy stack*** e como ele é configurado. 






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