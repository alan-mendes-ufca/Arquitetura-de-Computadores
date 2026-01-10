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
  - `memory`: transferência de dados entre diferentes níveis de memória (SDD -> RAM -> CACHE)
  - `writeback`: armazena os resultados no próprio processo

### Clock - FALTANDO

- O _ciclo de busca, decodificação e execução_ utiliza o clock do computador para regular seu ritmo, ou seja,
- `Pipeling`: permite executar instruções diferentes ao mesmo tempo

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

1. Liste e defina brevemente algumas das _técnicas_ usadas nos processadores atuais
   _para aumentar a velocidade_.

   1. **Pipelining** (Processamento em pipeline): **instruções** são processadas simultaneamente, cada uma em estágios diferentes

   2. **Memória Cache**: **armasena dados e instruções mais próximos à CPU**, reduzindo o tempo que demoraria para acessar a memória RAM

2. Caracterize brevemente a lei de Amdahl
3. Defina MIPS e FLOPS.
4. Desempenho da aplicação depende de quais atributos?
