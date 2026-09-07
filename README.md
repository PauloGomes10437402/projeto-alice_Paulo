# Projeto de Animação 3D - Alice 3

**Identificação:**
* **Aluno:** Paulo Meneghini de Oliveira Gomes
* **RA:** 10437402

---

## 1. Storyboard

### Sinopse
A animação retrata com humor a jornada de dois amigos rumo ao espaço sideral. Na base de lançamento, eles conferem os itens para a missão e percebem que, por preguiça e desatenção, deixaram de abastecer o combustível necessário, priorizando apenas ferramentas e cerveja. Mesmo cientes da situação, decidem partir. Ao chegarem ao vácuo espacial, o combustível acaba completamente; sem alternativas, eles aceitam o destino à deriva e resolvem abrir as cervejas enquanto a nave se perde na imensidão escura.

---

### Cenas da Animação

#### Cena 1: A Base de Lançamento e o Checklist
* **Cenário:** Plataforma em solo terrestre (`this.ground`) com a espaçonave estacionada ao lado dos personagens.
* **Personagens e Objetos:** `this.meloGabriel`, `this.gomesPaulo`, `this.spaceShip` e `this.camera`.
* **Ações e Diálogos:**
  1. A câmera enquadra `this.meloGabriel`, que pergunta sobre o combustível, ferramentas e propulsor.
  2. A câmera gira para `this.gomesPaulo`, que gesticula com o braço e confessa ter trazido apenas as ferramentas e a cerveja.
  3. A câmera dá um close em `this.meloGabriel`, que expressa espanto com a falta do combustível essencial.
  4. Sem recuar, ambos decidem partir imediatamente e a câmera se afasta.

#### Cena 2: No Espaço Sideral e a Pane Seca
* **Cenário:** Espaço sideral simulado por um fundo totalmente preto e vazio (atmosfera preta, sem chão visível).
* **Personagens e Objetos:** Apenas `this.spaceShip` e `this.camera` permanecem visíveis. Os personagens estão ocultos, representando que estão no interior da cabine.
* **Ações e Diálogos:**
  1. A atmosfera muda para preto (`BLACK`) e o chão (`this.ground`) e os personagens tornam-se invisíveis (`opacity = 0.0`).
  2. A espaçonave é redimensionada proporcionalmente via `resize` para simular a escala no espaço e a câmera enquadra a nave (`moveAndOrientToAGoodVantagePointOf`).
  3. Surge um balão de pensamento vermelho indicando a pane: `"*combustivel acaba*"`.
  4. Através da própria nave ocorrem os diálogos internos entre os dois tripulantes:
     * *"Trouxe cerveja ne?"*
     * *"Sim"*
     * *"Abre 2 ai..."*
  5. A câmera executa um recuo suave (`moveAwayFrom` em 10 metros), deixando a espaçonave à deriva no vazio escuro.

---

## 2. Planejamento da Implementação e Conceitos de POO

O projeto foi construído no **Alice 3**, explorando os principais fundamentos da **Programação Orientada a Objetos**:

### Classes e Objetos (Instâncias)
* `this` (Scene): Representa o ambiente/mundo que gerencia os demais objetos e propriedades globais.
* `this.ground`: Instância de `Ground`, representando a superfície terrestre da primeira cena.
* `this.camera`: Instância de `Camera`, manipulada para direcionar a perspectiva visual da narrativa.
* `this.meloGabriel` e `this.gomesPaulo`: Instâncias independentes derivadas da classe `Biped`. Cada uma mantém seu próprio estado, posição e articulações.
* `this.spaceShip`: Instância da classe de veículos espaciais, utilizada como objeto principal da segunda cena.

### Encapsulamento, Estado e Atributos
* **Manipulação de Estado em Tempo de Execução:**
  * `setAtmosphereColor(Color.BLACK)`: Altera a propriedade da atmosfera do mundo para simular o espaço sideral.
  * `setOpacity(0.0)`: Altera a visibilidade de `this.ground`, `this.gomesPaulo` e `this.meloGabriel`, simulando que os personagens agora estão dentro da nave sem precisar recriar um novo arquivo de projeto.
  * `resize(0.1 + 0.0)`: Altera a escala proporcional da nave nas três dimensões geométricas.

### Subpartes e Composição
* Acesso às partes internas dos modelos através de métodos de composição (*getters*), como `this.meloGabriel.getRightElbow()`, `this.gomesPaulo.getLeftElbow()` e `this.meloGabriel.getNeck()`, permitindo gesticulações realistas e independentes.

### Métodos, Troca de Mensagens e Parâmetros
* **Comunicação entre Objetos:**
  * `turnToFace(target)` e `moveToward(target, distance)`: Ajustam dinamicamente a posição e o ângulo da câmera em relação aos personagens.
  * `moveAndOrientToAGoodVantagePointOf(target)`: Posiciona automaticamente a câmera em um ângulo favorável de observação da nave.
  * `think(text, textScale, fontColor)`: Emite pensamentos estilizados no objeto da nave para representar eventos do sistema (pane de combustível em vermelho).
  * `say(text, duration)`: Apresenta as falas com controle de tempo de leitura.
  * `moveAwayFrom(target, distance, animationStyle)`: Executa o afastamento gradual da câmera com interpolação suave (`BEGIN_AND_END_GENTLY`).

### Controle de Fluxo
* **`Do in order`:** Estrutura sequencial que coordena a ordem cronológica estrita da animação (diálogos, ajustes de atmosfera, falhas no motor e encerramento com afastamento da câmera).
