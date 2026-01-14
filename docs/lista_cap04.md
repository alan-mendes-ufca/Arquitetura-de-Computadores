# Lista De Exercícios

### 1) Quais são as diferenças entre acesso sequencial, acesso direto e acesso aleatório?

- `Acesso Sequencial`: mais "mecânico", onde para acessar um dado em determinado endereço é necessário ler todos antes dele.
    - **Não existe teletransporte para o final**
    - Tempo de acesso variável: depende da localização do endereço na sequência ( *O(n)* )
    - Fitas magnéticas

- `Acesso Direto`: cada bloco de dados tem um endereço físico único, o branco de leitura pular direto para a "vizinhaça" e o disco gira até o setor específico. [Veja esse processo acontecendo aqui](https://youtube.com/shorts/EWJnkEesic8?si=PQMl7zvKQBXVI6tN)
    - Tempo de acesso variável: combina o **movimento mecânico** (braço de leitura + espera rotacional).
    - HDD

- `Acesso Aleatório`: **cada célula de memória tem um acesso eletrônico** (Linha A, Coluna B). O sistema acessa via sinais elétricos.
    - Tempo de acesso constante ( *O(1)* )
    - RAM e ROM

- `Acesso Associativo`: Uma tag é gerada com o endereço específico de um dado e o hardware executa essa busca de forma **simultanea** em todos os circuítos de memória
    - Muito rápida (constante), complexa e cara
    - Memória Cache

#### Resumo Comparativo: Métodos de Acesso à Memória

| Método | Analogia | Previsibilidade de tempo |
| :--- | :--- | :--- |
| **Sequencial** | Fita VHS (Rebobinar) | Muito variável (lento) |
| **Direto** | Disco Vinil (mover a agulha) | Variável (médio) |
| **Aleatório** | Armários numerados (local exato) | Constante (rápido) |
| **Associativo** | Gritar na sala (alguém levanta a mão) | Constante (instântaneo) |

---

### 2) Qual é a relação entre tempo de acesso, custo de memória e capacidade?
- `Quanto maior a velocidade de acesso, maior o cursto de memória e menor a capacidade.`

---

### 3) Como o `princípio de localidade` se relaciona com o uso de múltiplos níveis de memória?

- O princípio da localidade descreve uma **relação os programas e a memória**: programas tendem a acessar dados e instruções baseando-se no *tempo* e no *espaço*.
    - tempo: `programas tendem a acessar o mesmo dado mais de uma vez`
    - espaço: `dados são organizados próximos entri si na memória` (array, armazenado de forma sequencial e instruções, tambem sequênciais)

- Os **múltiplos níveis** de memória se referem a diferentes tecnologias de armazenamento: `Restradores -> Cache -> RAM -> SDD -> HDD`

> Dados contexto, essesr conceitos se relacionam pois **dados quentes**, utilizados mais frequentemente, tendem a ficar em **memória mais rápidas**.
E **dados armazenados de forma sequêncial desempenham melhor quanto a busca pelo seu endereço**. 

---

### 4) Quais são as diferenças entre `mapeamento` direto, mapeamento associativo e mapeamento associativo em conjunto?
- Organizações físicas do cache, literalmente a **arquitetura física do circuito**.
- Pra quê serve? **define quantas opções de posição existem para armazenar um bloco de memória**.
- Existem diferentes tipos de mapeamento físico pois cada um oferece diferentes **compromissos entre desempenho, custo e complexidade de hardware**.

- `mapeamento direto`: vários conjuntos são organizada em uma única via.
    - Regra: 

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
                        ├─────┼─────────────────┤
                Set 4   │ TAG │      DATA       │
                        ├─────┼─────────────────┤
                Set 5   │ TAG │      DATA       │
                        ├─────┼─────────────────┤
                Set 6   │ TAG │      DATA       │
                        ├─────┼─────────────────┤
                Set 7   │ TAG │      DATA       │
                        └─────┴─────────────────┘

    ```

- `mapeamento associativo`: cada via contém apenas um conjunto.
    - Regra: 
    ```
                Way 0           Way 1           Way 2           Way 3   
            ┌─────┬──────┐  ┌─────┬──────┐  ┌─────┬──────┐  ┌─────┬──────┐
    Set 0   │ TAG │ DATA │  │ TAG │ DATA │  │ TAG │ DATA │  │ TAG │ DATA |
            └─────┴──────┘  └─────┴──────┘  └─────┴──────┘  └─────┴──────┘  

    ```
- `mapeamento associativo em conjunto`: vários conjuntos são organizados em várias vias.
    - Regra: 
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
            ├─────┼──────┤  ├─────┼──────┤  ├─────┼──────┤  ├─────┼──────┤
    Set 4   │ TAG │ DATA │  │ TAG │ DATA │  │ TAG │ DATA │  │ TAG │ DATA │
            ├─────┼──────┤  ├─────┼──────┤  ├─────┼──────┤  ├─────┼──────┤
    Set 5   │ TAG │ DATA │  │ TAG │ DATA │  │ TAG │ DATA │  │ TAG │ DATA │
            ├─────┼──────┤  ├─────┼──────┤  ├─────┼──────┤  ├─────┼──────┤
    Set 6   │ TAG │ DATA │  │ TAG │ DATA │  │ TAG │ DATA │  │ TAG │ DATA │
            ├─────┼──────┤  ├─────┼──────┤  ├─────┼──────┤  ├─────┼──────┤
    Set 7   │ TAG │ DATA │  │ TAG │ DATA │  │ TAG │ DATA │  │ TAG │ DATA │
            └─────┴──────┘  └─────┴──────┘  └─────┴──────┘  └─────┴──────┘
    ```


---

### 5) Qual é a diferença entre localidade espacial e localidade temporal?
- localidade **espacial** refere-se a *possibilidade* de que dados próximos na memório sejam acessados quase ao mesmo tempo.
- localidade **temporal** define uma *probabilidade* de um dado acessado recentimento ser acessado novamente em um futuro próximo.

---

### 6) Defina e exemplifique o passo a passo da busca de uma palavra na memória cache
- O processador, ao executar uma instrução, buscará certo dado referido no escopo da instrução (000x55, endereço/tag referende a informação).
- Primeiramente, o dado é solicitado a memória cache.
    - Caso esteja em algum dos diferentes níveis de cache ele é retornado imediatamente, temos um `Cache Hit`: uma economia considerável de ciclos clock - um acesso muito mais rápido.
    - Na outra situação ocorre um `Cache Miss`, onde o Cache precisar fazer um acesso a memória principal, armazena o bloco de memória que continha aquele dado e o retorna para o processador.

---

### 7) Defina `Cache hit` e exemplifique
- É quando o processador busca um dado na memória e **encontra ele já presente no cache**.

- O acesso é **muito mais rápido** (1-5 ciclos vs 100+ ciclos da RAM).

**Exemplo:**
```
1. CPU pede: "Leia endereço 0x1000"
2. Cache verifica: TAG corresponde? ✓ Sim!
3. Cache retorna o dado imediatamente
4. HIT! (~1-3 ciclos)
```

**Cenário real:**
- Loop acessando `array[i]`: primeira iteração carrega o bloco inteiro
- Iterações seguintes: **HIT** (dados vizinhos já estão no cache por localidade espacial)

---

### 8) Defina `Cache miss` e exemplifique
- É quando o processador busca um dado na memória e **não encontra ele no cache**.
- Precisa buscar na **memória principal** (RAM), que é muito mais lenta.

**Exemplo:**
```
1. CPU pede: "Leia endereço 0x5000"
2. Cache verifica: TAG não corresponde? ✗ Não está aqui!
3. Cache busca na RAM (~100-300 ciclos)
4. Cache armazena o bloco
5. Cache retorna o dado
6. MISS! (penalidade de tempo)
```

**Cenário real:**
- Acessar posição `array[1000]` quando só `array[0-99]` estão no cache
- **MISS** → busca bloco na RAM → próximos acessos a `array[1000-1063]` são HITs


---

### 9) Defina hit ratio e exemplifique

---

### 10) Explique como a cache é organizada

---

### 11) Faça um exemplo do funcionamento do mapeamento direto

---

### 12) Faça um exemplo do funcionamento do mapeamento associativo

---

### 13) Faça um exemplo do funcionamento do mapeamento associativo por conjunto

---

### 14) Defina algoritmos de substituição e em quais mapeamentos eles são utilizados

---

### 15) Defina e exemplifique o funcionamento do algoritmo de substituição LRU - Least Recently Used

---

### 16) Defina e exemplifique o funcionamento do algoritmo de substituição Pseudo LRU - Least Recently Used

---

### 17) No contexto de sistemas com memória cache, quais são as duas principais políticas utilizadas para atualizar a memória principal após uma operação de escrita (Write Policy)? Defina cada uma

---

### 18) Dado a questão acima, exemplifique cada uma das politicas,