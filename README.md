# Arquitetura-de-Computadores

## [Como funciona um processador?](https://www.youtube.com/watch?v=16zrEPOsIcI&t=13s)


- `CPU é um componente que executa de forma cíclica instruções seguindo o ciclo: fetch → decode → execute → memory → writeback`.

- Diferentes processadores (IA, GPU, processadores antigos, unidades de processamento mobile) possuem um DNA tecnológico único: seu _projeto arquitetônico_ e um _princípio operacional básico_.

### Arquitetura de um processador

- O processador é formado por:

  - `Control Unity (CU)`: coordena todas as operações
    - Circuito de decodificação:
      - _Lê_ as instruções do Current Instruction Register (CIR) , _interpreta_ o binário da instrução e _retorna_ sinais de controle para realizar a instrução

  - `Registers`: memória muito rápida e pequena, localizada dentro do processador, que armazenam dados específicos (mais rápida que a memória CACHE)
    - Program Counter (PC): armazena o endereço da _próxima_ instrução a ser executadas
    - Current Instruction Register (CIR): armazena a instrução _atual_ que está sendo executada
    - Memory Address Register (MAR): armazena o endereço de memória do dado que será acessado (leitura ou escrita)

  - `CACHE`: otimização para evitar acessos a memória principal, guarda instruções e dados
    - Hierarquia de CACHE:
      1. **L1**: menor e mais rápida, utilizada para instruções e dados
      2. **L2**: Maior e um pouco mais lenta que a L1, utilizada quanto falta memória L1
      3. **L3**: Ainda maior (e mais lenta), é uma alternativa quando se falta L1 e L2, mas também permite que diferentes núcleos compartilhem dados entre si

  - `Arithmetical Logic Unit (ALU)`: circuito que realiza operações aritméticas (adição, subtração, multiplicação, divisão) e lógicas (AND, OR, NOT, XOR) sobre dados

### Princípio operacional básico

- O processador executa `instruções`, tarefas atômicas que compoem um algoritmo. Essas instruções são pré-definidas em um conjunto finito (o ISA - Instruction Set Architecture), ou seja, todo programa que rodamos no computador é construído com sequências dessas instruções disponíveis.
- Essas instruções são executadas seguindo três etapas principais:

  - `fetch`: utiliza o _program counter_ como referência para buscar qual instrução deve ser executada.
  - `decode`: chama o _circuito de decodificação_.
  - `execute`: executa a operação utilizando o ALU

- Alguns materiais adicionam outros dois passo, sigficativamente mais lentos que os anteriores:
  - `memory`: transferência de dados entre diferentes níveis de memória (SDD -> RAM -> CACHE -> Register)
  - `writeback`: armazena os resultados no próprio processo

### O que é `Clock`?
- Pulso elétrico oscilante, responsável pro **sincronizar** a atividade de um circuíto.
```
Pulso 1    Pulso 2    Pulso 3    Pulso 4
  │          │          │          │
  ▼          ▼          ▼          ▼
 FETCH  →  DECODE  →  EXECUTE  →  WRITE
```

- `Hz(Hertz)`: se diz respeito a uma unidade de medida de onda que `quantifica quantos ciclos acontecem por segundo`.
 Ou seja, a definir que um processador tem uma frequência de 2Ghz afirmamos ele executa 2 bilhões de oscilações (clock) por segundo.

- O _fetch -> decode -> execute -> memory -> writeback_ utiliza o clock do computador para regular seu ritmo, ou seja, cada etapa é SINCRONIZADA pelo clock, começando em um pulso específico. Cada etapa pode durar uma quantidade de ciclos diferente, sendo assim o clock marca QUANDO uma etapa começa, não obrigatoriamente quando termina.

- `Pipeling`: permite executar instruções diferentes ao mesmo tempo, em um mesmo ciclo
```
Ciclo 1  Ciclo 2  Ciclo 3  Ciclo 4  Ciclo 5  Ciclo 6  ...
Instr 1:│ FETCH  │ DECODE │EXECUTE │ WRITE  │        │
Instr 2:│        │ FETCH  │ DECODE │EXECUTE │ WRITE  │
Instr 3:│        │        │ FETCH  │ DECODE │EXECUTE │ 
Instr 4:│        │        │        │ FETCH  │ DECODE │
```

---

## Hierarquia de memória
- Um princípio básico: quanto mais rápida uma memória é, mais caro também é seu custo. Por isso, no sistema computacional, existem diferentes níveis de memória:
  1. Registradores: memória muito rápida e pequena, responsável por armazenar dados específicos e instruções.

  2. Memória CACHE: otimização que evita acessos a memória principal
      - L1: mais rápida e menor
      - L2: maior e mais lenta, opção direta quando não se tem mais espaço na L1
      -  L3: ainda maior e mais lenta, utilizada quando se falta memória em L1 e L2. A L3 ainda tem uma função mais específica: é utilizada para compartilhar dados entre núcleos (Multicore)

  3. Memória RAM (Random Accsess Memory) ou Principal: responsável pro guardar programar em execução.
      - Como as duas anteriores, a memória RAM é volátil, ou seja, os dados não ficam salvos em seu escopo: ao desligar o computador seu uso é zerado e sua capacidade se mantém intacta.
  
  4. Memória de Armazenamento ou Segundária: aqui nos referimos aos HDs e SSDs, responsáveis por armazenar dados brutos (hypermídea) e o próprio Sistema Operacional.
      - Não volátil: matém os dados gravados, mesmo sem energia

  5. Bônus: Memória Virtual: o processador aloca parte da memória segundária para servir de memória RAM.
      - Acontece quando a memória primária disponível no sistema se esgoda e é necessário concluir a tarefa.
      - O processamento fica considerávelmente mais lento, atrasando ciclos de clock e outros processos, mesmo assim ainda é um recursos muito útil em sistemas de baixo custo.

- No estágio de processamento `memory`, do processador, ocorre exatamente essa transferências de dados e instruções entre níveis diferentes de memória: SDD -> Memória RAM -> Memória Cache -> Resgistradores -> a tarefa é processada -> etapa de `writeback` os resultados são armazenados no próprio processo -> (CACHE) -> RAM -> SDD 

---

## Primeira aula - Introdução

1. Qual é a distinção entre a organização e a arquitetura do computador?

Referêm-se, por princípio, a _diferentes camadas de um sistema computacional_.

- _Arquitetura de computadores (Baixo nível)_: `o que o sistema faz (projeto lógico)?`

  - Conceituado por aspectos lógicos e abstratos que envolvem:
    - instruções (`um algoritmo são várias instruções`): `LOAD`, `ADD`, `STORE` - linguagem que o processador entende e executa;
    - `quantidade de bits` que representa determiando _tipo de dado_;
    - `registradores e endereçamento`
  - Impacto (se eu mudar, o que acontece?): **A camada de codificação precisa ser refeita, obedecendo as novas regras**.

- _Organização de computadores (Nível eletrônico)_: `como o sistema faz (implementação física)?`
  - Refere-se a _como a arquitetura é realizada na prática_, envolvendo tecnologia, componentes, circuitos e barramentos.
  - Impacto: **Performace e custo**;

2. Qual é, em termos gerais, a distinção entre a estrutura e a função do computador?

- A estrutura de um computador é, basicamente, os componentes físicos que permitem o computador realizar sua função;

3. Quais são as quatro funções principais de um computador?
   a. Processamento de dados;
   b. Armazenamento de dados;
   c. Comunicação (interna e externa);
   d. Controle (organizar as três operações descritas acima).

   - Para memorização, vamos definir um acrônimo: `APCC` (Armazenar, Processar, Comunicar, Controlar).

4. Liste e defina resumidamente os principais componentes estruturais de um computador.
   a. CPU (Central process unit);
   b. Memória RAM (Random access memory);
   c. I/O (mouse, teclado, monitor);
   d. Barrametos (conexões que permitem a troca de informações entre os componentess).

5. Liste e defina resumidamente os principais componentes estruturais de um processador
   a. Unidade de controle;
   b. Unidade lógica e aritmética;
   c. Registradores;
   d. Barramento, que conecta os três anteriores.

---

## Segunda aula - Desempenho

1. Liste e defina brevemente algumas das _técnicas_ usadas nos processadores atuais _para aumentar a velocidade_.

   1. **Pipelining** (Processamento em pipeline): dentro de um núcleo, instruções são processadas simultaneamente, cada uma em estágios diferentes.

   2. **Memória Cache**: otimização para evitar acessos a memória principal, tem como função armazenar dados e instruções.

   3. **Multicore**: ao invés de um único núcleo executar instruções sequencialmente, múltiplos núcleos trabalham simultaneamente em diferentes tarefas. Leia-se tarefas como instruções de processos, ou seja, vários núcleos podem trabalhar ao mesmo tempo em um único processo - esse processo precisa ser *paralelizável*.

   4. **Execução paralela**: multiplas instruções são processadas ao mesmo tempo, inclui *pipelining* e *multicore*. É importante que o processo/aplicação possa ser paralelizável, o que vai contra ao estado que uma instrução depende de um resultado anterior.

   5. **Execução fora de ordem**: caso não exista dependencia de dados, o processador reordena a execução de instruções. O que otimiza o pipelining evitando que a linha de produção fique ociosa esperando o resultado de uma instrução anterior, e, lógico, matém o resultado correto.

2. Caracterize brevemente a *lei de Amdahl*
- Define o *máximo* de ganho que se pode obter ao paralelizar uma aplicação, mostrando que a otimização tem uma *limitação fundamental*: a parte serial sempre será um gargalo. Assim, otimizar a parte serial é tão importante quanto paralelizar a parte paralelizável.
- `Speedup = 1 / ( S + P/n)`
  - **S** = fração serial (não paralelizável) do programa
  - **P** = fração paralelizável 
  - **n** = número de núcleos
  > Leia-se: a aceleração máxima é 1 sobre a fração serial somada a fração peralelizável dividida pelo número de núcleos 

3. Defina MIPS e FLOPS.
- **MIPS** (Million Instructions Per Second): `Frequência do clock * Instruções por ciclo / 10^6`
- **FLOPS** (Floating Point Operations Per Second): métrica importante para *aplicação científicas e gráficas*.
  - MEGAFLOPS: 10⁶
  - GIGAFLOPS: 10⁹
  - TERAFLOPS: 10¹²

4. Desempenho da aplicação depende de quais atributos, atenha-se ao desenvolvimento de software?

- **Conjunto de instruções do processador (ISA - Instruction Set Architecture)**: instruções são operações pré-definidas que formam a base de qualquer programa, sendo uma sequência dessas instruções. A quantidade e tipo de operações pré-definidas interfere no desempenho de uma aplicação pois permitem executar operações complexas em um único ciclo.
  - Menos instruções necessárias = menos ciclos de clock = execução mais rápida

- **Linguagem de programação escolhida**: reduz (ou aumenta) camadas de abstração entre o código e a linguagem de máquina. Linguagens de baixo nível (C, Assembly) são mais próximas do hardware; linguagens de alto nível (Python, Java) têm mais abstração.

- **Eficiência do compilador**: traduz o código-fonte em código binário otimizado, explorando características do hardware.

- **Habilidade do programador**: a forma como o desenvolvedor escreve o código, explora recursos de hardware (cache, paralelismo) e da linguagem influencia diretamente o desempenho final.