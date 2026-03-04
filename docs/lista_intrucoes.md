## Lista De Exercícios

### Visão Geral

```
┌─────────────────────────────────────────────────────────────────┐
│                          ISA                                    │
│                                                                 │
│  Elementos da instrução:       Locais de operandos:             │
│  • Opcode                      • Registradores (rápido)         │
│  • Operando fonte              • Memória RAM (lento)            │
│  • Operando destino            • Imediatos (na instrução)       │
│  • Próxima instrução (PC)      • Dispositivos E/S               │
│                                                                 │
│  Questões de projeto:          Tipos de instrução:              │
│  • Completeza                  • Transferência de dados         │
│  • Formato/tamanho             • Aritmética/Lógica              │
│  • Registradores               • Shift                          │
│  • Endereçamento               • Controle de fluxo ← (Q7)       │
│  • Tipos de dados              • Comparação                     │
│                                • E/S / Sistema                  │
│                                                                 │
│  Mais endereços → instruções menores em quantidade, mais longas │
│  Menos endereços → instruções mais em quantidade, mais curtas   │
│                                                                 │
│  Tudo isso junto define: compatibilidade, desempenho,           │
│  complexidade de hardware e software                            │
└─────────────────────────────────────────────────────────────────┘
```

#### 1) Quais são os elementos típicos de uma instrução de máquina? Defina cada um deles.

```
 31          20 19   15 14  12 11    7 6       0
┌──────────────┬───────┬──────┬───────┬─────────┐
│   imm[11:0]  │  rs1  │funct3│  rd   │ opcode  │
│   12 bits    │ 5 bits│3 bits│ 5 bits│  7 bits │
└──────────────┴───────┴──────┴───────┴─────────┘
```

- **Opcode**: qual o **tipo de instrução**? (aritmética/lógica, transferência, comparação, etc)
  - Número binário que o processador decodifica para saber **o que fazer/qual operação realizar**;
    ```
    add  x1, x2, x3
    ↑
    Opcode → "realize uma adição"
    ```

- **Referência a operando fonte**: indica **de onde vem os dados**(registrador, imediato/constante ou endereço) que a função vai processar;

  ```
  add  x1, x2, x3
          ↑   ↑
      fonte 1  fonte 2  →  os dados que serão somados
  ```

- **Referência de operando de resultado**: onde o resultado será armazenado;

  ```
  add  x1, x2, x3
        ↑
      resultado →  o registrador que deve conter o resultado
  ```

- **Referência à próxima instrução**: geralmente o processador já tem definido a próxima instrução no PC (Program Counter); entretanto, em intruções de salto (`JUMP`) ele vem definido:
  ```
  beq  x1, x2, LABEL   # Se x1 == x2, pula para LABEL
               ↑
       Referência explícita à próxima instrução
  ```

---

#### 2) Que tipos de locais podem manter operandos de origem e destino?

```
┌──────────────────────────────────────────────────────────────────┐
│  1. REGISTRADORES                                                │
│     • Dentro do processador                                      │
│     • Exemplo: x1, x2, EAX, RAX                                  │
├──────────────────────────────────────────────────────────────────┤
│  2. MEMÓRIA PRINCIPAL (RAM)                                      │
│     • Fora do processador                                        │
│     • Referenciada por endereço: lw x1, 4(x2)                    │
├──────────────────────────────────────────────────────────────────┤
│  3. IMEDIATOS (constantes na instrução)                          │
│     • O valor está embutido nos próprios bits da instrução       │
│     • Exemplo: addi x1, x2, 10  ← o 10 é imediato                │
├──────────────────────────────────────────────────────────────────┤
│  4. DISPOSITIVOS DE E/S (I/O)                                    │
│     • Em arquiteturas com instruções de I/O dedicadas            │
│     • Ex: arquiteturas x86 com IN/OUT                            │
│     • Lê de ou escreve em portas de dispositivos externos        │
└──────────────────────────────────────────────────────────────────┘

---

Registrador  →  ~1 ciclo       ████████████████████  ← mais rápido
Cache L1     →  ~4 ciclos      ████████████
Cache L2     →  ~12 ciclos     ████████
Cache L3     →  ~40 ciclos     █████
RAM          →  ~200 ciclos    ██                    ← mais lento



```

---

#### 3) Se uma instrução contém quatro endereços, qual poderia ser o propósito de cada endereço?

- `OPERAÇÃO A, B, C, D`
  - Operation code
  - Source Operand Reference
  - Destination Operando Reference
  - Next instruction

---

#### 4) Cinco questões importantes no projeto do conjunto de instruções

| #   | Questão                       | Resumo                                                                                                          |
| --- | ----------------------------- | --------------------------------------------------------------------------------------------------------------- |
| 1   | **Completeza das operações**  | Quais operações o processador suporta nativamente? (ex: incluir ou não multiplicação, divisão, ponto flutuante) |
| 2   | **Formato das instruções**    | As instruções terão tamanho fixo ou variável? Quantos bits?                                                     |
| 3   | **Número de registradores**   | Quantos registradores existem? Mais registradores = mais rápido, porém chip maior                               |
| 4   | **Modos de endereçamento**    | De quais formas o processador pode localizar um operando? (imediato, registrador, memória, base+offset...)      |
| 5   | **Tipos de dados suportados** | Quais tipos o processador manipula nativamente? (inteiro, ponto flutuante, caractere, vetor...)                 |

---

#### 5) Que tipos de operandos são típicos nos conjuntos de instruções de máquina?

- `unsigned int`, `int`, `float`, `char`, `&`, `bool`

---

#### 6) Que tipos de instruções são típicos nos conjuntos de instruções de máquina?

- **Registradores**: _variáveis_ físicas dentro do processador;
  - `add x1, x2, x3 `

- **Imediatos**: _constantes_ definidas dentro da instrução, não precisam ser buscadas pois já estão definidas;
  - `addi x1, x2, 10 #10 é imediato`
- **Endereços de memória**: definem dados endereçados que precisam ser buscados na memória _RAM_;
  - `lw x1, 4(x2)      # Carrega palavra da memória no endereço (x2 + 4) para x1`
  - `sw x1, 8(x3)      # Armazena x1 na memória no endereço (x3 + 8)`

---

#### 7) Por que são necessárias instruções de transferência de controle?

- Sem transferência de controle, **não existiria estrutura lógica (condicional, loops, funções e exceções)**. Todo programa seria uma lista fixa de operações executadas uma única vez, em ordem — sem condições, sem repetição, sem funções.

- Em x86, os equivalentes seriam `jmp`, `je/jne/jg...`, `call` e `ret`.

---

#### 8) Para que serve o ISA (Instruction Set Architecture)?

- Todo software já criado pode ser definido como um conjunto de instruções pré definidas, essas instruções são **identificadas e executadas pelo processador**; imagine uma calculadora com milhares de operações já definidas em fábrica - esse é o processador; Por analogia, essas instruções servem de blueprint em relação a uma atividade específica e sua existência define que o processador consegue executar aquela operação nativamente com o melhor desempenho possível.
  - Instruções definem o que o processador sabe fazer;
  - A quantidade de instruções pode variar de acordo com arquitetura (x86-64, ARM) e geração do processador(mais antiga ou mais recente);
  - Atualmente, processadores Intel e AMD são padronizados seguindo o mesmo conjunto de instruções (ISA);

```
Alto nível:    Python / Java / C
     ↓         Compilador / Interpretador
Baixo nível:   Assembly
     ↓         Assembler
Máquina:       ISA (0s e 1s que o processador executa)
     ↓
Hardware:      Transistores, circuitos, lógica digital
```

---

#### 9) Qual a vantagem e desvantagem de utilizar mais endereços nas instruções?

```
┌─────────────────────────────────────────────────────────┐
│  MAIS ENDEREÇOS POR INSTRUÇÃO                           │
├───────────────────┬─────────────────────────────────────┤
│  ✅ VANTAGENS     │  ❌ DESVANTAGENS                    │
├───────────────────┼─────────────────────────────────────┤
│ Programas mais    │ Instruções mais longas (mais bits)  │
│ curtos — uma      │                                     │
│ instrução faz     │ Hardware de decodificação mais      │
│ mais coisas       │ complexo e caro                     │
│                   │                                     │
│ Código mais       │ Mais tempo para buscar a instrução  │
│ expressivo e      │ na memória (instruction fetch)      │
│ legível           │                                     │
│                   │ Menos espaço para o campo de cada  │
│ Menos instruções  │ endereço → menos registradores      │
│ para programar    │ endereçáveis                        │
│ uma tarefa        │                                     │
└───────────────────┴─────────────────────────────────────┘
```

---

#### 10) Qual a vantagem e desvantagem de utilizar menos endereços nas instruções?

```
┌─────────────────────────────────────────────────────────┐
│  MENOS ENDEREÇOS POR INSTRUÇÃO                          │
├───────────────────┬─────────────────────────────────────┤
│  ✅ VANTAGENS     │  ❌ DESVANTAGENS                    │
├───────────────────┼─────────────────────────────────────┤
│ Instruções mais   │ Programas mais longos — precisam    │
│ curtas e simples  │ de mais instruções para a           │
│                   │ mesma tarefa                        │
│ Hardware de       │                                     │
│ decodificação     │ Mais instruções = mais acessos      │
│ mais simples      │ à memória = mais lento              │
│                   │                                     │
│ Mais fácil de     │ Código menos expressivo             │
│ fazer pipeline    │                                     │
│ (paralelismo)     │ Mais pressão sobre registradores    │
│                   │ (resultados intermediários)         │
│ Cada instrução    │                                     │
│ executa mais      │                                     │
│ rapidamente       │                                     │
└───────────────────┴─────────────────────────────────────┘
```

---

#### 11) O que as escolhas sobre repertório de instruções, formatos de instruções e registradores definem?

- As escolhas sobre repertório de instruções, formatos e registradores definem o **contrato imutável entre o software e o hardware** — determinando o que pode ser computado, como o compilador gera código, qual o desempenho máximo atingível e quão complexo e eficiente o processador será. Em outras palavras: `definem a identidade e a personalidade de toda a arquitetura`.
