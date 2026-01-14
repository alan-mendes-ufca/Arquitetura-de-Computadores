
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

---

## Terceira aula - Memória Cache

1. Indique a(s) resposta(s) errada(s).
    1. **Com o avanço dos vários tipos de memórias, vai `desaparecer` por completo a hierarquia de memória.**
      - A hierarquia de memória permanecerá existindo, pois existe uma relação muito concisa nas tecnologias de memória: quanto mais rápidas, maior a complexidade de hardware e maior será seu custo (também menor será sua capacidade).

    2. A vantagem do mapeamento direto é a sua simplicidade.

    3. **Outra `vantagem` do mapeamento direto é o fenômeno de thrashing.**
      - thrashing é um fenômeno onde ocorre substituições/conflitos constantes e excessivas.

    4. No mapeamento associativo, a linha que contém o bloco desejado é obtida rapidamente pois todos os tags são comparados em paralelo.
    
    5. **Outra vantagem do mapeamento associativo é a simplicidade na implementação da circuitaria para o acesso associativo.**
     - O mapeamento assiciativo requer um hardware mais complexo e caro.

2. Indique a(s) resposta(s) errada(s).
    1. O mapeamento associativo por conjunto reúne as vantagens do mapeamento direto e o mapeamento associativo.
    2. O mapeamento associativo por conjunto é o mais usado em processadores modernos.
    3. **Para escolher a linha para ser substituída, é comum executar-se um algoritmo de substituição ótimo em que todas as possíveis linhas são testadas como objeto de substituição.**
    4. Write-through é uma técnica mais conservadora para manter a consistência. Mas write-back minimiza escrita na memória e ainda mantém a consistência embora tardiamente.