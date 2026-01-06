# Arquitetura-de-Computadores

## Primeira aula - Introdução

1. Qual é a distinção entre a organização e a arquitetura do computador?

Referêm-se, por princípio, a _diferentes camadas de um sistema computacional_.

- _Arquitetura de computadores (Baixo nível)_: `o que o sistema faz (projeto lógico)?`
  - atributos do sistema que são **visíveis** ao programador de baixo nível:
    - instruções (`um algoritmo são várias instruções`): `LOAD`, `ADD`, `STORE` - linguagem que o processador entende e executa;
    - `quantidade de bits` que representa determiando _tipo de dado_;
    - mecanismos de endereçamento de memória: camada lógica que busca o `registrador do processador`, que calcula _onde_ buscar ou salvar um dado.
  - Impacto (se eu mudar, o que acontece?): **A camada de codificação precisa ser refeita, obedecendo as novas regras**.

---

- _Organização de computadores (Nível eletrônico)_: `como o sistema faz (implementação física)?`
  - unidades operacionais e suas interconexões que **realizam** as especificações de arquitetura:
    - barramentos;
    - tecnologia e tipo de memória;
    - clock.
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
