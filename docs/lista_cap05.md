# Lista De Exercícios

### 1) Porque o termo Estático e Dinâmico entre DRAM e SRAM?

- Dynamic RAM: o termo dinâmico faz referência ao seu modo de funcionamento:
    - Composição: transistor + capacitor (transistor controla o acesso ao capacitor)
    - O capacitor armazena o estado de positivo ou negativo. Quando carregado (bit ligado), lentamente ele vai perdendo tensão, ao chegar perto ao limiar (2v a 3v) ocorre um REFRESH para 5v. Capacitores desgarregados (bit desligado) também são verificados e "refrescados" no ciles, pois eles podem ser recarregados lentamente por diferentes fatores (ruído eletromagnético, temperatura, etc).
    ```
    Refresh Periódico (64ms)
    - Linha A: 5v -> 4.2v -> 3.5v -> REFRESH -> 5v
    - Linha A: 0v (Descarregado) -> 0v -> 0v -> REFRESH -> 0v 
    ```
    - O ato de ler um dado na DRAM destrói esse dado. O que também prejudica sua performace.
        - Aqui entra o papel do transistor, ele é responsável por conectar o capacitor ao bitline (fio condutor que conectar o capacitor ao circuito de R/W). 
        A perda de dados ocorre pois nessa conexão os elétrons fluem para o bitline e descarregando o capacitor, ao verificar a aproximação ao limiar o controlador de memória recarrega o capacior.

 - Static RAM
    - Composição: 1 flip-flop (6 transistores)
    - Como os flip-flops, diferente dos capacitores, não perdem carga/dados não é necessário realizar um ciclo de REFRESH. Por isso são estáticos.
    - Sua leitura não é destrutiva, contribuindo para o desempenho.
---
### 2) DRAM e SRAM são voláteis ou não voláteis?
Sim, ambas são volátei: sem energia perdem os daos armazenados.
---
### 3) Qual é a diferença entre DRAM e SRAM em termos das características como velocidade, tamanho e custo?
O SRAM é mais veloz, com um hardware maior (6 transistores), porém mais caro.
O DRAM é mais lento (ciclo de REFRESH, leitura destrutiva), com hardware menor (transistor + capacitor) e mais barato.

---
### 4) Um bit em DRAM é composto pelo que?
Por uma porta FLIP-FLOP (6 transistores)

---
### 5) Um bit em SRAM é composto pelo que?
- Capacitor + Transistor

---
### 6) O que é o refresh na DRAM?
- O caracitor é carregado (bit ligado) ou descarregado (bit desligado).

---
### 7) Para que serve o Address Line?
- O barramento de endereço é formado por um conjunto de Address Lines.
    - Serve para a transmissão de endereços para lida e escrita na memória.
    - Limitam a quantidade de acessos a diferentes blocos de memória.
```
CPU ──┬─ Address Line 0 ─┐
      ├─ Address Line 1 ─┤
      ├─ Address Line 2 ─┤  ← Barramento de Endereço
      ├─ Address Line 3 ─┤     (32 linhas = 32 bits)
      │     ...          │
      └─ Address Line 31─┘
                │
                ▼
              DRAM

Cada linha = 1 bit do endereço
32 linhas = endereço de 32 bits
Combinações = 2^32 blocos de memória acessáveis
```

---
### 8) Dizemos que a DRAM é mais densa, porque?
- DRAM utiliza 1 transistor e 1 capacitor por bit, assim dizemos que ela é mais densa pois cabem mais bits numa menor área fisica.
```
Em um chip de 1 cm²:

DRAM (densa):
┌─┬─┬─┬─┬─┬─┬─┬─┐
├─┼─┼─┼─┼─┼─┼─┼─┤  Muitas células em pouco espaço
├─┼─┼─┼─┼─┼─┼─┼─┤
└─┴─┴─┴─┴─┴─┴─┴─┘
├─ Cabe: 8 GB de memória
└─ Muito compacta

---

SRAM (espaçosa):
┌───────┬───────┬───────┬───────┐
├───────┼───────┼───────┼───────┤  Poucas células ocupam muito espaço
├───────┼───────┼───────┼───────┤
└───────┴───────┴───────┴───────┘
├─ Cabe: ~1 GB de memória
└─ Muito maior para mesma capacidade
```

---
### 9) Quais são as diferenças entre EPROM, EEPROM e memória flash?
Memórias não-Voláteis:
- EPROM: Pode ser programada múltiplas vezes. Os dados são TOTALMENTE apagados com radiação UV.

- EEPROM: Pequena evolução da EPROM, permite que os dados sejam apagados eletricamente, é mais veloz e permite apagar de forma parcial.

- Memória flash: Evolução do EEPROM (mais velocidade, capacidade e resistência). Utilizado em SSDs, pendrives, smatphones, etc.

---
### 10) A memória ROM pode ser formada baseadas em quais portas?
- NOR e NAND

---
### 11) O que é bit de paridade?
- Um bit extra é adicionado a um grupo de bits para verificar se houve corrupção de dados; O número total de bits 1 deve ser par.
- O bit paridade é obtido fazendo uma operação XOR com os bits do dado enviado.
- Não é eficaz quando a quantidade de erros afetados é par e não retorna qual bit está errado (para um possível correção).
---
### 12) Quantos bits são necessários para detectar um erro de transmissão de dados?
- Na transmissão de dados entre computadores é utilizado a função checksum. O checksum é calculado a partir dos dados a serem transmitidos e é enviado junto deles, ao final o receptor faz a mesma operação e verifica se os checksums batem.

- O tamanho de um checksum pode varia de acordo com o nível de confiabilidade (detecção de erros) que o sistema quer, sendo 1 ou mais bytes.

---
### 13) Em quais o bit de paridade não consegue detectar o erro de transmissão de dados?
O método não detecta erros quando há uma quantidade par de bits errados.

---
### 14) Quantos bits são necessários para corrigir um erro de transmissão de dados?
Não há um número fixo de bits; depende da quantidade de dados transmitidos.

---
### 15) Qual operação utilizamos para calcular o bit de paridade?
- O bit paridade é obtido fazendo uma operação XOR com os bits do dado a ser enviado.

---
### 16) No código de Hamming, a posição dos bits de verificação P não é aleatória; eles ocupam as posições que são potências de 2 (1, 2, 4, 8...). Se estivermos utilizando uma palavra de dados de 16 bits, qual será a posição (número do bit) do último bit de verificação necessário?

Fórmula: 2^r >= m + r + 1

2^x >= 16 + x + 1
2^x >= 17 + x 
2^5 >= 17 + 5 -> 32 >= 22

Portanto, são necessários 5 bits paridade.

P1 - validará xxx1
P2 - validará xx1x
P4 - validará x1xx
P8 - validará 1xxx
P16 - - validará 1xxxx

Resposta final: a posição do último bit de paridade necessário é 16.

---
### 17) Suponha que uma palavra de dados de 8 bits armazenada na memória seja 11000010. Usando o algoritmo de Hamming, determine quais bits de verificação seriam armazenados na memória com a palavra de dados. Mostre como você chegou a sua resposta.

11000010

Aplicando a fórmula: 2^x >= 8 + x + 1, logo x = 4. Assim são necessários 4 bits de paridade.

`P1 P2 D3 P4 D5 D6 D7 P8 D9 D10 D11 D12`
 ?  ?  1  ?  1  0  0  ?  0  0   1   0

P1 [xxx1] = 1 + 1 + 0 + 0 + 1 = 1 
P2 [xx1x] = 1 + 0 + 0 + 0 + 1 = 0
P4 [x1xx] = 1 + 0 + 0 = 1
p8 [1xxxx] = 0 + 0 + 1 + 0 = 1

---
### 18) Para uma palavra de 8 bits 00111001, os bits de verificação armazenados com ela seriam 0010. Suponha, quando a palavra for lida da memória, que os bits de verificação são calculados como 1010. Qual palavra de dados foi lida da memória?

`P1 P2 D3 P4 D5 D6 D7 P8 D9 D10 D11 D12`
 ?  ?  0  ?  0  1  1  ?  1  0   0   1

P1 = 0 + 0 + 1 + 1 + 0 = 0
P2 = 0 + 1 + 1 + 0 + 0 = 0
P4 = 0 + 1 + 1 + 1 = 1
P8 = 0

Ocorreu um erro: os bits, quando recalculados foram: 1010

P8 P4 P2 P1
Esperado: 0  0  1  0
Lido:     1  0  1  0
         ---  ---  ---  ---
Diferença: 1  0  0  0  (XOR)

`P1 P2 D3 P4 D5 D6 D7 P8 D9 D10 D11 D12`
 1  0  0  1  0  1  1  1  1  0   0   1
                      X

* O erro aconteceu em um bit de paridade, logo os dados continuáram intactos

---
### 19) Considere uma palavra de dados de 8 bits 00111001
### a) Calcule os bits de paridade
### b) Ao ler essa palavra algum tempo depois, o sistema recuperou a seguinte sequência de bits de dados: 00111011. Mostre como identificar o bit errado

---
### 20) Quantos bits de verificação serão necessários se o código de correção de erro de Hamming for usado para detectar erros de único bit em uma palavra de dados de 1.024 bits?

---
### 21) Escolha um número M entre 5 a 11.
### a) Invente um número de M bits e escreva o código de Hamming.
### b) Agora erre um bit neste código e use a técnica para corrigir o erro.
### OBS: Obviamente não é para olhar a primeira parte para descobrir qual bit errado