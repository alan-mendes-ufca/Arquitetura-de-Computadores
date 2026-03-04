## Lista De Exercícios

#### 1) Liste três classificações gerais de dispositivos externos ou periféricos

- **Preiféricos de `I/O`**: _comunicação_ com os usuários do computador
  - Monitores, teclado, mouse, webcam, impressora
- **Periféricos de `Armazenamento`**: _comunicação_ com equipamentos internos
  - SSD, HD externo, pendrive USB
- **Periféricos de `Rede/Comunicação`**: _comunicação_ com dispositívos remotos
  - Placa de rede (Ethernet, WIfi) e Bluetooth

---

#### 2) Quais são as principais funções de um módulo de E/S?

- De forma geral, o módulo de entrada e saída é uma _ponte inteligente_, responsável de coordenar operação entre o processador e memória com dispositívos/periféricos
  - Define uma interface com o processador e a memória (**Interface Interna**)
  - Define outra inferface com os periféricos (**Interface Externa**)

```
┌─────────────────────────────────────┐
│       PROCESSADOR/BARRAMENTO        │
└────────────────┬────────────────────┘
                 │
           INTERFACE I/O
        (Sinais, protocolos,
         especificações)
                 │
┌────────────────▼────────────────────────────┐
│   CONTROLADOR/MÓDULO DE ENTRADA E SAÍDA     │
└────────────────┬────────────────────────────┘
                 │
           INTERFACE I/O
        (Portas, conectores)
                 │
┌────────────────▼───────────────────┐
│         PERIFÉRICOS EXTERNOS       │
└────────────────────────────────────┘
```

- Observação: leia-se interface como um **ponte de comunicação** entre dois dispositivos. Ela é responsável por:
  - **`Conectar`** dois componentes diferentes
  - **`Padronizar`** a forma de interação

---

#### 3) Liste e defina brevemente três técnicas para realizar E/S.

- `I/O Programada`: o processador executa continuamente instruções para verificar o status do dispositivo de E/S. O programa testa repetidamente um bit de status até que o dispositivo sinalize que está pronto.
  - Simples, mas ineficiente pois o processador perde muitos ciclos de clock esperando o processamento mais lento do dispositivo de I/O.

- `I/O Dirigida por interrupções`: o processador emite um comando de entrada e saída e continua a executar outras instruções. Quando o módulo estiver pronto um sinal de interrupção é enviado, o processo que estava em atividade é pausado (com seu estado salvo) e o CPU retoma a atividade anterior.
  - Melhora o desempenho anulando o tempo de espera descrito anteriormente;
  - O estado atual da tarefa é salva no Program Counter (PC) e outros registradores.

- `Acesso Direto à Memória (DMA)`: um controlador DMA transfere os dados diretamento entre os periféricos e a memória, sem intervenção do processador.

**Resumo Geral**:

| Técnica                       | Eficiência | Complexidade | Uso do Processador |
| ----------------------------- | ---------- | ------------ | ------------------ |
| E/S Programada                | Baixa      | Simples      | 85-95%             |
| E/S Orientada por Interrupção | Média      | Moderada     | 20-40%             |
| Acesso Direto à Memória (DMA) | Alta       | Complexa     | 5-15%              |

- as porcentagens menores acorrem pelo uso de interfaces (módulos)

---

#### 4) Qual é a diferença entre E/S mapeada na memória e E/S independente?

- Ambos **não utilizam memória RAM**, a diferenç estre os dois se diz respeito ao uso (ou não) do espaço de endereçamento.
  - O espaço de endereçamento não é uma estrutura física, é apenas um VALOR: **a quantidade de endereços que pode ser gerados com a combinação de x bits**.
  - E o que acontece quando um endereço está fora do espectro de atuação de um processador? Ocorre uma exceção. Para solucionar essa limitação o Sistema Operacional é responsável por definir uma **memória virtual**, uma abstração que 'engana' o processador limitando sua visão.

```
Registrador:                 Espaço de Endereçamento:
┌─────────────────┐         ┌──────────────────┐
│ É uma CAIXA     │         │ É o TAMANHO DO   │
│ que armazena    │         │ GUARDA-ROUPA     │
│ dados           │         │ (capacidade)     │
└─────────────────┘         └──────────────────┘

Registrador PC = 0x1000     Processador tem 32 bits
(contém um endereço)        (pode acessar até 4 GB)
```

- `Mapeada`: **OCUPAM PARTE** do espaço de endereçamento (**barramento de endereços**) o que reduz a memória disponível (um endereço a menos que a memória RAM poderia utilizar).

```
PROCESSADOR
                             │
                    ┌────────┼────────┐
                    │        │        │
              [Instrução   [Dados]  [Endereço]
               NORMAL]

                    │        │        │
                    ↓        ↓        ↓
            ┌──────────────────────────────┐
            │    CHIPSET (Decodificador)   │
            └──────────────────────────────┘
                             │
                             │
                    BARRAMENTO DE ENDEREÇOS
                    (32/64 bits - ÚNICO!)
                             │
         ┌───────────────────┼───────────────────┐
         │                   │                   │
         ↓                   ↓                   ↓
    RAM: 0x0-0x7FFF    Placa Vídeo:        ROM: 0xF0000
                       0xB0000-0xBFFFF

    ┌──────────┐      ┌──────────┐      ┌──────────┐
    │ Memória  │      │Dispositivo│      │BIOS/ROM  │
    │ Principal│      │Mapeado    │      │          │
    └──────────┘      └──────────┘      └──────────┘

   TODOS OCUPAM O MESMO BARRAMENTO DE ENDEREÇOS
   (O Chipset decodifica o endereço e ativa o certo)
```

- `Independente`: utilizam um espaço totamente diferente, um **barramento de Portas**. Traz a necessidade de intruções especiais e é mais complexo de programar.

```
PROCESSADOR
                             │
                    ┌────────┼────────┐
                    │        │        │
              [Instrução   [Dados]  [Endereço]
               IN/OUT]

                    │        │        │
                    ↓        ↓        ↓
            ┌──────────────────────────────┐
            │    CHIPSET (Decodificador)   │
            └──────────────────────────────┘
                    │        │        │
         ┌──────────┘        │        └──────────┐
         │                   │                   │
         ↓                   ↓                   ↓
    BARRAMENTO          BARRAMENTO         BARRAMENTO
    DE PORTAS        DE DADOS              DE ENDEREÇOS
   (16 bits)         (8/16/32 bits)       (32/64 bits)
         │                   │                   │
         │                   │                   │
    ┌────┴────┐         ┌────┴────┐        ┌────┴────┐
    │          │         │         │        │         │
    ↓          ↓         ↓         ↓        ↓         ↓
Porta Serial Porta      Dados   Dados      RAM      ROM
0x3F8      Paralela    de E/S            0x0-8K   0xF0000
           0x378

   DISPOSITIVOS EM        │        MEMÓRIA
   ESPAÇO SEPARADO        │      (mesmo espaço)
```

- o uso de cada estratégia está relacionado ao periférico:
  - Memory-Mapped (Transferência de alto volume): periféricos internos (SSD, GPU) e de comunicação (Placa de Rede). Estes utilizam o DMA como estratégia de comunicação.
  - I/O independende (Transferências de baixo volume): periféricos de I/O (comunicação com o Humano).

---

#### 5) Quando um módulo de DMA toma o controle de um barramento, e enquanto ele retém o controle do barramento, o que o processador faz?

- O processador entra em estado de espera, interrompendo os ciclos de fetch e execution.

```
Processador                DMA
    |                      |
    |--- Requisição DMA ---|
    |    (IRQ/Signal)      |
    |                      |
    | Cede Controle do Bus |
    |<--------BUS----------|
    |                      | ← Transfere dados
    |                      | ← Memória ↔ Periférico
    |     (Aguardando)     |
    |                      |
    |--- Sinal de Fim -----|
    |    (Interrupt)       |
    |                      |
    |--- Retoma Bus -------|
```

---

#### 6) Em praticamente todos os sistemas que incluem módulos de DMA, o acesso por DMA à memória principal recebe prioridade mais alta que o acesso da CPU à memória principal. Por quê?

- DMA trata fluxos contínuos de dados que não podem esperar (alto risco de currupção);
  - Sem cache ou registradores, o que ocorre é uma tranferência DIRETA para a memória.
- CPU pode esperar sem perder dados.

---

#### 7) No diagrama de blocos de um dispositivos externos existem 3 componentes, quais são? Defina a funcionalidade de cada um deles

- `Lógica de controle`: controla a operação do dispositivo em resposta ao módulo de I/O

- `Buffer`: associado ao transdutor, armazena dados de forma temporária. O transduto trabalha em tempo físico, enquanto o controlado em tempo digital, assim o buffer é responsável por sincronizar essas duas velocidades.

- `Transdutor`: converte analógico ↔ digital
  - Microfone: som (analógico) -> bits (digital)
  - Monitor: bits (digital) -> luz (analógico)

```
Periférico externo (disco):

Meio Externo → [Transdutor] → [Buffer] → [Lógica] → Módulo I/O
(dados)       (converte)    (guarda)    (controla)
```

---

#### 8) As principais funções ou requisitos para um módulo de E/S podem ser divididas em 5 categorias, quais são?

Esses 5 atributos, juntos, garantem confiabilidade para essa operação:

- Controle e temporização
- Comunicação com o processador
- Comunicação com o periférico
- Buffering de dados
- Detectação de errors

---

#### 9) Para que serve a função de controle e temporização?

- **`Sincronizar diálogo`**: cumpre a função de um mediador de debates: garante que os dois participanes não "falem" ao mesmo tempo, nem ultrapassem seu tempo de argumentação

---

#### 10) Para que serve a função de controle de Buffering de dados?

- **`Sincronizar envio e recebimento de dados`**: compensa a desparidade de velocidade:
  - **processador -> periférico**: recebe rajadas rápidas de informações, mas as transmite em um ritmo lento para não afogar o módulo
  - **periférico -> processador**: intercepta rajadas mais lentas e as acumula, evitando que a memória principal fique bloqueada por muito tempo

---

#### 11) Para que serve a função de Detecção de erro?

- **`Confiabilidade`**: monitora a integridade dos dados, avisando ao processador sobre a presença de possíveis falhas:
  - Papel emperrando na impressora ou bits com interferência em comunicação com periféricos externos

---

#### 12) Quais são os 5 passos da operação de leitura em um dispositivo de E/S?

- Programada (Polling) - **CPU verifica continuamente o estado do dispositivo**

1. CPU verifica estado do I/O
2. Se pronto → requisita leitura
3. Se não → aguarda iterativamente
4. Dados capturados e salvos em memória

**Problema:** CPU fica bloqueada ✗

---

- Interrupção - **Dispositivo avisa quando está pronto**

1. CPU requisita leitura
2. CPU trabalha em outros processos
3. Dispositivo envia sinal de interrupção
4. CPU interrompe, lê dados e restaura contexto

**Vantagem:** CPU livre durante espera ✓

---

DMA (Direct Memory Access) - **Controlador DMA transfere dados direto para memória**

1. CPU requisita ao controlador DMA
   - CPU também define o endereço que os dados devem ser armazenados
2. CPU trabalha em outros processos
3. DMA assume controle do barramento
4. Dados transferem direto para memória
5. DMA interrompe CPU quando termina

**Vantagem:** CPU completamente livre ✓

#### 13) O que queremos dizer quando falamos sobre nível de abstração dos módulos de E/S?

- Determina a estratégia de apresentação do módulo ao processador, prodendo ser mais simples ou mais flexível;
- Quanto menor o nível maior o controle do processador sob o periférico

---

#### 14) Como funciona o fluxo de operação da E/S programada?

- Programada (Polling) - **CPU verifica continuamente o estado do dispositivo**

1. CPU verifica estado do I/O
2. Se pronto → requisita leitura
3. Se não → aguarda iterativamente
4. Dados capturados e salvos em memória

**Problema:** CPU fica bloqueada ✗

---

#### 15) Como é o comportamento do módulo de E/S na E/S programada?

- O módulo responde solicitações constantes sobre seu estado e mantém sua responsabilidade de captar os dados do periférico

---

#### 16) Qual o impacto do processador ao usar a técnica de E/S programada?

- Muitos ciclos de clock são perdidos devido à espera de um sinal de estado positivo

---

#### 17) Quais são os 4 passos do fluxo de operação de leitura da técnica de E/S dirigida por interrupção?

- Interrupção - **Dispositivo avisa quando está pronto**

1. CPU requisita leitura
2. CPU trabalha em outros processos
3. Dispositivo envia sinal de interrupção
4. CPU interrompe, lê dados e restaura contexto

**Vantagem:** CPU livre durante espera ✓

---

#### 18) Quais são as vantagens e desvantagens da E/S dirigida por interrupção?

- O cpu é livre durante o processo de esperado, entretando ainda fica responsável por buscar e armazenar os dados

---

#### 19) Qual a motivação para utilizar o Acesso Direto à Memória (DMA) ?

- O cpu fica totalmente livre durante o estágio de espera e armazenamento

---

#### 20) Como se dá o passo a passo de uma operação utilizando DMA?

DMA (Direct Memory Access) - **Controlador DMA transfere dados direto para memória**

1. CPU requisita ao controlador DMA
   - CPU também define o endereço que os dados devem ser armazenados
2. CPU trabalha em outros processos
3. DMA assume controle do barramento
4. Dados transferem direto para memória
5. DMA interrompe CPU quando termina

**Vantagem:** CPU completamente livre ✓
