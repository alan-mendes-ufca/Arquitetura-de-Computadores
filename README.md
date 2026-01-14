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

## Memória Cache
- Acessos repetitivos a memória principal degradam o desempenho de uma aplicação, pois esse acesso pode demorar muitos ciclos de clock. Para **otimizar** o processo o CPU pode copiar blocos de dados da memória principal para seu cache - fazendo modificações por associação, depois atualizando a cópia original. 

- Níveis de cache: L1(pequeno, rápido e caro), L2(médio, moderado e mais barato) L2(grande, lento e ainda mais barato).

- Exemplo de execução: 
  - o primeiro passo é a CPU verificar se um determinado endereço está no cache. 
  - Caso não esteja pois o processador aindo não o salvou temos um `Cache Miss`. 
  - Nesse caso, os dados serão copiados da memória principal para a memória cache. Os endereços seguintes ao solicitado também serão salvos (princípio da localização no espaço).
    - Quando o processador precisar do próximo valor na posição, ele já estará no cache, contribuindo para o desempenho - `Cache Hit`.

### Cache de dados
- O cache organiza seus dados em linhas (32, 64 ou 128 bytes).
  - `linha de cache = [TAG] [DADOS] [FLAGS]`
    - `[TAG]` = endereço relativo a memória principal de onde os dados vieram

### Mapeamento de cache
- Refere-se organização física do cache, diferentes arquiteturas para os circuítos: mapeamento `direto`, `associativo` ou `associativo em conjunto`. Definem como blocos da memória principal são organizados e localizados no componente.

- `mapeamento direto`: cada linha funciona como um conjunto individual de 1-way.
  - Para defirnir a localização de um bloco é necessário fazer o cálculo: `posição = número do bloco MOD número de linhas/conjustos`
    - Considere 1024 blocos na memória principal, para 256 linhas de cache. Nesse contexto, os blocos de número **0, 256, 512 vão competir pelo mesma posição**. Apenas um desses pode estar armazenado no cache por vez naquela posição (**linha 0**).
    - `Substituição cega e automática`.

    ```
                                    Way 0
                        ┌─────┬─────────────────┐
                Set 0   │ TAG │      DATA       │
                        ├─────┼─────────────────┤
                Set 1   │ TAG │      DATA       │
                        ├─────┼─────────────────┤
                Set 2   │ TAG │      DATA       │
                        ├─────┼─────────────────┤
                Set 3   │ TAG │      DATA       │
                        └─────┴─────────────────┘

    ```
- `mapeamento associativo`: um único conjunto contendo todas as linhas da cache (N-way, onde N = total de linhas)
    - **Não há fórmula!** O bloco pode ir em **qualquer linha livre**. 
    - Se o cache está cheio, escolhe-se um endereço para ser sobreescrito usando uma `política de substituíção`:
      - LRU (Leasty Recent Used)
      - FIFO (First In Firt Out)
      - Random
    ```
                Way 0           Way 1           Way 2           Way 3   
            ┌─────┬──────┐  ┌─────┬──────┐  ┌─────┬──────┐  ┌─────┬──────┐
    Set 0   │ TAG │ DATA │  │ TAG │ DATA │  │ TAG │ DATA │  │ TAG │ DATA |
            └─────┴──────┘  └─────┴──────┘  └─────┴──────┘  └─────┴──────┘  

    ```

- `mapeamento assciativo em conjunto`: vários conjuntos (de várias linhas) inseridos em várias vias (potências de dois).
  - `Conjunto = número do bloco MOD número de conjuntos`.
  - Dentro do conjunto, pode ser alocado em qualquer linha daquele conjunto.
  - Se ocorrer de todas as 4 linhas estare ocupadas aplica-se uma **política de substituição** dentro daquele conjunto.
    ```         
                Way 0           Way 1           Way 2           Way 3
            ┌─────┬──────┐  ┌─────┬──────┐  ┌─────┬──────┐  ┌─────┬──────┐
    Set 0   │ TAG │ DATA │  │ TAG │ DATA │  │ TAG │ DATA │  │ TAG │ DATA │
            ├─────┼──────┤  ├─────┼──────┤  ├─────┼──────┤  ├─────┼──────┤
    Set 1   │ TAG │ DATA │  │ TAG │ DATA │  │ TAG │ DATA │  │ TAG │ DATA │
            ├─────┼──────┤  ├─────┼──────┤  ├─────┼──────┤  ├─────┼──────┤
    Set 2   │ TAG │ DATA │  │ TAG │ DATA │  │ TAG │ DATA │  │ TAG │ DATA │
            ├─────┼──────┤  ├─────┼──────┤  ├─────┼──────┤  ├─────┼──────┤
    Set 3   │ TAG │ DATA │  │ TAG │ DATA │  │ TAG │ DATA │  │ TAG │ DATA │
            └─────┴──────┘  └─────┴──────┘  └─────┴──────┘  └─────┴──────┘
    ```


---
