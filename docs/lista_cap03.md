## Lista De Exercícios

1) Quais são os três principais componentes do computador que
estão interconectados?
- CPU
- Memória
- I/O

2) Quais os dois principais motivos da importância da visão de alto
nível do computador?
- Abstraí a complexidade de uma visão de baixo nível, que trás consigo conceitos complexos de arquitetura, fornecendo uma base para compreender a natureza e o funcionamento interno de um compudor.
- Permite o desenvolvimento de software independente de quesrtões físicas de hardware

3) Praticamente todos os projetos de computadores modernos são
baseados em conceitos desenvolvidos por? Quais seus conceitos
principais?
- Os computadores modernos de baseiam no *modelo teórico de Von Neumann*, seguindo o princípio do programa armazenado e componentes básicos decritos: 
    - CPU (Central Unit, Arthmetic Logic Circuit)
    - Memória
    - Equipamentos de input/output

4) O que é um programa? Defina
- Um programa é um conjunto de algoritmos/instruções que unidos formam uma ferramenta que resolvem um problema
- entrada -> processamento -> saída

5) Como os sinais de controle devem ser fornecidos?
- No estágio de decodificação, dentro do processador, o circuíto de decode fica responsável por traduzir o código de máquina das intruções e retornar esses sinais de controle que coordenam os devidos circuítos para a execução da tarefa.

6) Para que serve o Registrador de Instrição (IR) e o Contador de
Programa (PC)?
- IR: responsável por armazenar o endereço da instruçãop que está sendo executada no momento
- PC: armazena o endereço da próxima instrução que será executada

7) Quais os dois passos da função básica realizada pelo
computador?
- armazenar dados e processar instruções

8) Como um ciclo de busca funciona?
- O ciclo de busca tem como objetivo extrair o programa que será executado, por meio do registrador Current Instruction Register, já definido anteriormente

9) Exemplifique o funcionamento do ciclo de busca
- Um sinal de clock é liberado sincronizando o início do processamento de uma determinada instrução, e, lógico, suas demais etapas
- A primeira etapa é o `fetch` que, por meio do circuíto IR, busca a primeira instrução que deve ser executada

10) Os bits do formato de instrução são divididos em duas partes,
quais são?
- bits de controle: indicam qual operação deve ser executada
- bits de dados: sobre quais dados a operação deve ser realizada

11) Os bits do formato inteiro são divididos em duas partes, quais
são?
- 1 bit para o sinal: positivo ou negativo
- bits de magnitude: valor numérico

12) No contexto da visão de alto nível, exemplifique o
funcionamento do processador.
- Na visão de alto nível o processador é o componente responsável por coordenar os demais e processar dados e instruções, sendo descrito como o cérebro do computador

13) Liste e defina resumidamente os estados possíveis que
definem a execução de uma instrução
- `fetch` -> `decode` -> `execute` -> `memory` -> `writeback`

14) Liste e defina resumidamente duas técnicas para lidar com
múltiplas interrupções.
- **Mascaramento de interrupções**: durante o tratamento de uma interrupção o processador desabilitas outras temporariamente.
- **Fila de interrupções**: interrupções que não podem ser tratadas imediatamento ficam armazenadas em uma fila.

15) Qual o objetivo e a motivação para o uso de interrupções?
Interrupções de processos são fornecidas em primeiro lugar como um modo de melhorar a eficiência e aproveitamento do processador.
- Componentes externos de I/O são muito mais lentos que o processador, assim o CPU ficaria ocioso esperando esses dispositivos terminarem seu processamento. Para corrigir esse disperdício de uso, o processador pausa o trabalho nesse processo e inicia ou dá continuidade a outro.
Depois, ao receber um sinal eletríco do componente de i/o ele retorna para a execução daquela atividade.

16) Exemplifique um programa sem interrupção
- Programas independentes de dispositivos de i/o, como: algoritmos que executam internamente na CPU.

17) Exemplifique um programa com interrupção curta
- Acesso ao cache ou a memória principal.

18) Exemplifique um programa com interrupção longa
- Entrada de teclado.

19) Defina barramento de dados e o que ele limita
- Transmitir dados entre os componentes
- CPU <-> Memória <-> I/O

20) Defina barramento de endereço e o que ele limita
- Transpote de endereços que indicam onde os dados serão lidos ou escritos
- CPU -> RAM

21) Defina o barramento de controle e qual é sua função principal
na interconexão do computador
- Coordena as operações do sistema: leitura, escrita, clock e interrupções

22) Por que a fase de busca da instrução deve sempre vir antes da
fase de execução da instrução
- Por que a fase de busca é responsável por encaminhar a instrução que será processada para a execução

23) Qual a principal desvantagem (em termos de desempenho do
processador) do método de E/S sem interrupções
O processador fica ocioso, perdendo "milhares" de clicos clock que poderiam estar resolvendo alguma outra instrução.