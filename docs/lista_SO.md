## Lista De Exercícios

#### 1) O que é um sistema operacional?

- Um SO, ou sistema operacional, é o software fundamental e tem como responsabilidades:
  - gerenciamento do hardware/recursos (`kernel`);
  - abstratir essa comunicação para o usuário final (`interface gráfica`);
  - acoplar outros tipos de software com funcionalidades específicas;

---

#### 2. Liste e defina de forma resumida os principais serviços fornecidos por um sistema operacional

- **Criação de programas**: entrega aos desenvolvedores ferramentas/abstrações que facilitam sua atividade
  (editores de código e depuradores);

- **Inicalização de aplicativos**: abstrai o ciclo de processamento realizado pela CPU, além de outras abstrações desenvolvidas pelo próprio SO como a tradução de código para binário (compilação);

- **Acessos a dispositivos de I/O**: traduz comandos complexos de hardware em operações simples (`read/write`) para que programadores consigam trabalhar com inputs e outputs sem dominar a complexidade eletro-eletônica;

- **Confiabilidade**: controla o acesso à dados/recursos a usuários não altorizados ou mal intencionados;

- **Identificação de erros**: erros são salvos como via de aprimoramento de software.

---

#### 3. Liste e defina de forma resumida os principais tipos de **escalonamento** do sistema operacional.

- O SO precisa decidir qual **processo** vai utilizar o **processador** em cada momento, essa atividade é chamada de _escalonamento_. Para resolver esse problema existem diferentes abordagens:
  - `FIFO (First In First Out)`: funciona exatamento como uma **fila**!
    - ✅ Muito simples
    - ❌ Um processo muito longo bloqueia a execução de outros
    - 📊 Fácil calcular o tempo de espera

  - `SJF (Shortest Job First)`: o trabalho que tiver o menor número de processos será executado primeiro
    - ✅ Minimiza o tempo de espera MÉDIO
    - ❌ INANIÇÃO: trabalhos longos nunca rodão
    - 📊 Impossível calcular o tempo de espera
      (trabalhos menores podem se emplilhar sobre um maior)

  - **`RR (Round Robin) = FILA CIRCULAR + QUANTUM`**: É O MAIS UTILIZADO em sistemas reais, consiste em tornar o processador um _recurso compartilhado_, onde todos os processos tem acesso por uma determinada fatia de tempo (**`QUANTUM`**)
    - ✅ NÃO sofre inanição
    - ✅ Justo
    - ❌ O quantum precisa ser muito bem balanceado para evitar **`OVERHEAD (eficiência)`**

---

#### 4. Qual é a diferença entre um processo e um job?

JOB:
└─ "O que você QUER fazer"
└─ Tarefa abstrata, planejamento
└─ Está na fila esperando

PROCESSO:
└─ "O que o SO está FAZENDO agora"
└─ Execução concreta e dinâmica
└─ Tem PID, memória, registradores, contexto (metadados)

---

#### 5. Qual é o propósito da troca de processos na memória?

```
FUNCAO swapping(novo_processo)
    ENQUANTO (RAM_disponível < RAM_necessária) FAÇA
    processo ← ENCONTRE_PROCESSO_BACKGROUND()

        SE (processo != NULL) ENTÃO
            SALVE processo para DISCO
            RAM_disponível ← RAM_disponível + tamanho(processo)
        FIM_SE

    FIM_ENQUANTO

    CARREGUE novo_processo na RAM
```

- A RAM é um recurso limitado, então mover um processo que não está sendo utilizado para o disco é uma estratégia inteligente de eficiência.

---

#### 6. A alocação de um processo na memória principal é sempre contíguo?

- Não, estratégia mais utilizada em SOs modernos é a `PAGINAÇÃO`.
  - É uma abstração/funcionalidade que contorna a alocação de memória de forma contínua na mamória;
  - Dividir processos em PEQUENOS PEDAÇOS de tamanho fixo e espalhá-los na memória, usando um índice (tabela) para saber onde cada pedaço está.

---

#### 7. O sistema é organizado de forma hierárquica, quais são os componentes dessa hierarquia?

- A hierarquia do sistema operacional consiste em um conjunto de camadas, da mais abstrata para a mais próxima ao hardware:
  - `Aplicações do usuário`: navegadores editores e jogos;
  - `Utilitários e bibliotecas`: APIs, shells, gerenciamento de arquivos
  - `Kernel`: gerenciamente de processos, memória, arquivos e I/O;
  - `Hardware`: processador, memória e periféricos

```

┌─────────────────────────────┐
│   APLICAÇÕES DO USUÁRIO     │  ← Menos privilégio
├─────────────────────────────┤
│  UTILITÁRIOS/BIBLIOTECAS    │
├─────────────────────────────┤
│      KERNEL (SO)            │  ← Mais privilégio
├─────────────────────────────┤
│       HARDWARE              │  ← Físico
└─────────────────────────────┘
```

---

#### 8. Defina a responsabilidade de cada um dos elementos da hierarquia

- `Aplicações do usuário`: permite executar desde **ferramentas digitais de trabalho** ou **entretenimento**, ou serviços do SO por meio de chamadas do sistema;

- `Utilitários e bibliotecas`: **ferramentas de gerenciamento do sistema**, podendo ter um controle menor ou maior(administrador, que tem controle root);

- `Kernel`: gerencia todo os hardware e adiciona abstrações importantes para aumentar sua eficiência;

- `Hardware`: executa instruções do processador e armazena dados.

---

#### 9. Quais são os serviços oferecidos pelo SO?

- **Desenvolvimento de programas**
- **Inicialização de aplicações**
- **Acesso simplificado a I/O**
- **Confiabilidade**
- **Identificação de erros**

---

#### 10. Defina o ISA (Instruction Set Architecture):

- Todas os programas construídos por meio de linguagens de programação podem ser caracterizados como um conjunto lógico de instruções pré-definidas, essas instruções pertêncem ao processador e sua quantidade pode variar de acordo com geração e arquitetura.

- Por analogia, instruções são como um blueprint de operações específicas, se o processador tem uma instrução para determinada atividade signica que ele sabe realizar aquilo com a maior eficiência possível.

- O que acontece quando um programa utiliza uma instrução não definida no conjunto? A aplicação é interrompida abruptamente com um lancamento de erro **`Erro: SIGILL (Signal: Illegal Instruction)`**

---

#### 11. Defina API (Application Programming Interface):

- Conjunto de regras e protocolos programados que estabelecem comunicação entre aplicações;
- Define regras e padrões para a trasmissão e recebimento de dados no fluxo cliente <-> servidor;
  - REST, por exemplo, é um estilo de arquitura que define regras que APIs devem se comprometer, uma API RESTFULL é uma interface que respespeita todas as espicificações definidas.

---

#### 12. Quais são os quatro pilares de hardware para que o Sistema Operacional não seja apenas um 'convidado' no computador?

- `Interrupções (Gerenciamento de I/O)`: SO tem acesso a interrupção para gerenciar e padronizar

  ```
  Evento físico:     Clique do mouse
                         │
                         ▼
  SO REAGE:          Interrupção recebida
                         │
                         ▼
  SO GERENCIA:       ┌─ Prioridade alta?
                     ├─ Qual app recebe?
                     ├─ Agendar em fila?
                     └─ Executar agora ou depois?
  ```

- `Proteção de memória (Confiabilidade)`: isolamento entre processos, inclindo o próprio SO

- `Modos de Operação (Hierarquia)`: especifica a hierarquia do sistema, definindo responsabilidades para o kernel, root ou usuário;

- `Relógio/timer (Sincronização)`: permite definir e validar o QUANTUM, além de sincronizar todo o sistema (síncrono x assíncrono)

```
        ┌─────────────────────────┐
        │  CONTROLE TOTAL DO SO   │
        │  sobre o HARDWARE       │
        └────────────┬────────────┘
                     │
        ┌────────────┴──────────────┐
        │                           │
   ┌────▼───────┐    ┌──────────┐   │
   │Interrupções│    │Proteção  │   │
   │            │    │ Memória  │   │
   └────────────┘    └──────────┘   │
        │                           │
   ┌────▼──────┐   ┌──────────┐     │
   │  Modos de │   │ Relógio/ │     │
   │Operação   │   │  Timer   │     │
   └───────────┘   └──────────┘     │
        │                           │
        └────────────┬──────────────┘
                     │
              ╔══════╩═════════╗
              ║  Necessários   ║
              ║  para SO       ║
              ║  ter controle  ║
              ╚════════════════╝
```

---

#### 13. O que é a funcionalidade de escalonamento do SO?

- O escalonamento é um especificação gerir a interação de processos com o processador, como se inúmero cliente quisessem acessar o mesmo recurso, essa funcionalidade dita como o multitarefas se comportará bem como o desempenho de todo sistema. Principais estratégias de escalonamento:

* escolanmento de curto prazo: **qual proceso usa a CPU?**
* médio prazo: **qual programa trazer para a RAM?**
* longo prazo: **qual JOB entra na fila?**

---

#### 14. Porque no escalonamento de médio prazo remove processos ativos?

- `Swapping`: Qual programa trazer para a RAM?

- Por que utilizar swapping? A memória RAM é um recurso limitado dentro do sistema computacional e frequentemente é necessaŕio se ter mais memória do que o disponível para manter processos carregados na memória, assim a estratégia de swapping é importante para gerenciar a disponibilidade da memória e manter o conjunto funcionando de maneira eficiente.

---

#### 15. O que o Sistema Operacional faz com a CPU quando escalona um processo para ser executado usando o escalonador de curto prazo?

- `Dispatcher`: Qual tarefa usa o CPU AGORA?
- Quando um novo processo é escalonado para o processador é necessário rodar uma rotina de `context switch`; nessa operação dados do processo em execução são salvos e dados do novo processo são carregados.

---

#### 16. Qual papel do gerenciamento de memória?

- O **gerenciamento de memória** é responsável por manter em ordem reduzir **desperdícios de espaço e evitar ociosidade do processador**.

---

#### 17. Quais os tipos de particionamento de memória que temos? Defina cada um deles

- Refere-se a forma como o SO divide a memória RAM entre processos em execução;

- `Estático`: a memória é dividida em um número pré definido de blocos em tamanhos fixos. Processos, mesmo que pequenos, são fixados em um determinado tamanho que não preenchem totalmente, portanto temos um desperdício de memória chamado de `fragmentação geral (total de fragmentações internas)`;
  - **Memória livre > número de partições livres**;
  - `Fragmentação interna`: refere-se ao espaço dentro de uma partição reservada que não é utilizado;
  - Uma solução seria ter diferentes partições de diferentes megabytes; mesmo assim esse sistema não resolve todos os problemas pois fragmentação (mesmo com menor fragmentação geral) e a possibilidade de faltar partições continuam ocorrendo.

- `Dinâmico`: permite que o sistema operacional crie novas partições para cada processo ou solicitação de memória, com o tamanho da partição correspondente ao tamanho da solicitação feita;
  - `Fragmentação externa`: processos deixam um legado, regiões de espaço vazio que não podem ser utilizas pois não são contínuas na memória; esse problema é resolvido com `compactação`, onde o SO realoca os processos removendo partições fixas e deixa um espaço contínuo na sequência (computacionalmente caro);
  - `Algoritmo de alocação`: outro tipo de soluções que substituem a compactação, dado menor overhead;
    - _First Fit_: de cima para baixo aloca no primeiro espaço encontrado
    - _Next fit_: aloca após a última alocação (fila circular)
    - _Best fit_: encontra o bloco de memória que melhor se adapta ao requisitado (inteligente)
    - _Worst fit_: aloca o processo no maior bloco de memória disponível

- `Segmentação`:
  - segmentos são trocados entre o disco e a memória quando necessário;
  - um segmento só pode ser susbtituído por outro de mesmo tamanho ou menor;
  - **Fragmentação externa**
  - Grandes segmentos podem ser rejeitados pela memória com muita frequência

- `Paginação`:
  - a memória é dividida em pequenas, exatas seções chamadas de `páguinas` (4kb);
  - a memória física também é dividida em pequenos blocos de 4kb, `frames`;
  - um processo pode ser divido em várias páguinas, que não são necessáriamente blocos contínuos;
  - cada programa tem sua própria visão da memória, chamado de memória lógica;
  - o sistema operacional matém uma tabela de com informações sobre quais locais lógicos correspondem a um endereço real;
  - `Memória Virtual`: funcionalidade que consiste em complementar a RAM com memória secundária. Com pouca memória principal disponível o número de tranferência de páguinas para o disco pode ser muito alto, deixando o sistema extremamente lento pois o SO passa mais tempo trocando as páguinas do que executando os processos(Trashing).

```
┌──────────────┬──────────────┬──────────────┬──────────────┬──────────────┐
│ Aspecto      │ Estático     │ Dinâmico     │ Segmentação  │ Paginação    │
├──────────────┼──────────────┼──────────────┼──────────────┼──────────────┤
│ Tamanho fixo │ Sim (problema)│ Não (melhor) │ Não (lógico) │ Sim (4KB)   │
│ Fragmentação │ INTERNA      │ EXTERNA      │ EXTERNA      │ NENHUMA      │
│ Proteção     │ Básica       │ Básica       │ Boa          │ Excelente    │
│ Uso Moderno  │ Raro         │ Raro         │ Raro         │ PADRÃO ⭐    │
│ Compartilhar │ Difícil      │ Difícil      │ Fácil        │ Fácil        │
│ Complexidade │ Baixa        │ Média        │ Alta         │ Média        │
└──────────────┴──────────────┴──────────────┴──────────────┴──────────────┘
```

---

#### 18. Qual problema acontece com o tempo quando se usa particionamento de memória variável?

- Como os processos são armazenados de forma contínua na memória, ao finalizar aquela tarefa resta um bloco de tamanho fixo como resíduo.

---

#### 19. Paginação aparece como uma solução para resolver o problema que acontece com o tempo quando se usa particionamento de memória variável. Defina a paginação e o que ela faz:

- A páginação corrige os resíduos de blocos não contínuous deixados por processos. O SO cria uma abstração da memória física chamada de memória lógica, onde blocos físicos (frames, 4kb) contínuos ou não são reoganizados e mapeados em páguinas (4kb) teoricamente contínuos; Processos são fragmentados em várias páguinas.
  - Esse mapeamento de frames para páguinas é armazenado em tabelas índice x endereço

---

#### 20. O que é memória virtual e que tipo de paginação ela emprega?

- A memória virtual é uma ferramenta definida pelo particionamento de paginação, basicamente ocorre um swapping onde ao invés de um processo inteiro ser alocado no disco apenas algumas páguinas são liberadas.

---

#### 21. Qual princípio da suporte a ideia da paginação por demanda? Defina esse princípio.

- O princípio da localidade temporal e espacial, justifica o uso da paginação por demanda pois programas utilizam pouca memória de cada vez.

```
Leitor PDF (100 MB código total):
├─ Demand Paging do SO:
│  └─ Carrega páginas 4 KB sob demanda
├─ Lazy Loading do Programa:
│  └─ Carrega features sob demanda
└─ Resultado: ~20 MB em RAM, não 100 MB
```

---

#### 22. Qual problema pode acontecer na memória virtual que pode deixar seu computador lento?

Quando o sistema tem pouca memória RAM, ocorre um processo de swapping de páguinas constrante:

```
Troca A → Remove B → Precisa B → Troca B → Remove A...
[CICLO INFINITO]
```

Ainda, pelo fato do acesso a memória de disco ter um alto overhead, o sistema fica muito lento.
