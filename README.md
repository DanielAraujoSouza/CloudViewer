# CloudViewer

Classe [JavaScript](https://developer.mozilla.org/docs/Web/JavaScript) que abstrai toda a complexidade necessária para criar uma visualizador de nuvens de pontos 3D em um página web. Este visualizador faz uso das tecnologias web [Three.js](https://threejs.org/), [Bootstrap](https://getbootstrap.com/) e [Font Awesome](https://fontawesome.com/), para criar uma interface amigável de visualização de nuvens de pontos em 3D. Além da biblioteca principal, Three.js, também é utilizado o controlador de câmera, [TrackballControls](https://threejs.org/docs/#examples/en/controls/TrackballControls), que possibilita mover, rotacionar e aplicar zoom à cena, utilizando o cursor do mouse.

## Índice

- [Dependências](#dependências)
- [Uso](#uso)
- [Métodos](#métodos)
  - [addCloud](#addcloud)
  - [fitCanvasToCloudGroup](#fitcanvastocloudgroup)
  - [removeCloudByLabel](#removecloudbylabel)
  - [setAutoScale](#setautoscale)
  - [setCameraAxis](#setcameraaxis)
  - [setPointSize](#setpointsize)
  - [startAnimation](#startanimation)
  - [stopAnimation](#stopanimation)
  - [reset](#reset)
  - [updateCanvas](#updatecanvas)
- [Exemplo](#exemplo)
- [Tipos de Dados](#tipos-de-dados)
  - [Cloud OBJ](#cloud-obj)

## Dependências

- Versão 5 do **Bootstrap** (CSS e JavaScript);
- Core do **Three.js**;
- Bilbioteca CSS do **Font Awesome 5**;
- Complemento **TrackballControls** do Three.js.

## Uso

Após importar a classe CloudViewer, em seu codigo JavaScript, basta instanciá-lo passando o identificador do container HTML onde será gerado. Por exemplo, para inserir um visualizador no container `#canvas1`:

```js
import CloudViewer from "/src/CloudViewer.js";

const myViewer = new CloudViewer("#canvas1");
```

## Métodos

### addCloud

Método para adicionar uma nuvem de pontos 3D ao visualizador.

```js
myViewer.addCloud(cloud, label, color);
```

- **[IN] cloud** - Objeto correspondente a nuvem de pontos ([Cloud OBJ](#cloud-obj)).
- **[IN] label** - Identificador da nuvem de pontos ([String](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)).
- **[IN] color** - Coloração utilizada nos pontos ([String](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)). Este parâmetro pode ser uma representação:
  - Hexadecimal - Ex: `#FF25AC`;
  - String RGB - Ex: `rgb(255, 0, 0)` ou `rgb(100%, 0%, 0%)`;
  - Nomes de cores no X11 (todas as letras em **minúsculo**) - Ex: `red`, `skyblue`, `darkgray`;
  - String HSL - Ex: `hsl(0, 100%, 50%)`.

### fitCanvasToCloudGroup

Método para enquadrar o conjunto de nuvens, adicionadas no visualizador, ao espaço de visualização (canvas).

```js
myViewer.fitCanvasToCloudGroup(forced);
```

- **[IN] forced** - Se esse argumento for `True` o enquadramento será realizado mesmo que o ajuste automático esteja desabilitado na interface do visualizador. ([Boolean](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Boolean)).

### removeCloudByLabel

Método remover uma nuvem do visualizador.

```js
myViewer.removeCloudByLabel(cloudLbl);
```

- **[IN] cloudLbl** - Identificador da nuvem de pontos ([String](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)).

### setAutoScale

Método para ativar ou desativar o redimensionamento automatico. Caso esteja ativos, esse redimensionamento será aplicado ao adicionar novas nuvens, modificar tamanho dos pontos e alterar abertura da câmera.

```js
myViewer.setAutoScale(value);
```

- **[IN] value** - `true` ativa e `false` desativa ([Boolean](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Boolean)).

### setCameraAxis

Define o eixo padrão da câmera. Este eixo é levado em consideração é feito o enquadramento.

```js
myViewer.setCameraAxis(axis);
```

- **[IN] axis** - Eixo ortogonal (X, Y ou Z) ([String](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)).

### setPointSize

Define o tamanho de um ponto no espaço de visualização.

```js
myViewer.setPointSize(pointSize);
```

- **[IN] pointSize** - Tamanho do ponto (([Number](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number)).

### startAnimation

Inicia o loop de animação.

```js
myViewer.startAnimation();
```

### stopAnimation

Para o loop de animação.

```js
myViewer.stopAnimation();
```

### reset

Remove todas as nuvens do visualizador.

```js
myViewer.reset();
```

### updateCanvas

Executa uma iteração do loop de animação.

```js
myViewer.updateCanvas();
```

## Exemplo

Página HTML:

```html
<!DOCTYPE html>
<html>
  <head>
    <title></title>
    <link
      rel="stylesheet"
      href="https://cdn.jsdelivr.net/npm/bootstrap@5.0.1/dist/css/bootstrap.min.css"
      integrity="sha384-+0n0xVW2eSR5OomGNYDnhzAbDsOXxcvSN1TPprVMTNDbiYZCxYbOOl7+AMvyTG2x"
      crossorigin="anonymous"
    />
    <link
      rel="stylesheet"
      href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.3/css/all.min.css"
    />
  </head>
  <body>
    <div class="row">
      <div class="h2">CloudViewer Exemple</div>
    </div>
    <div class="row">
      <div class="col-6 vh-50">
        <div id="canvas1"></div>
      </div>
      <div class="col-6 vh-50">
        <div id="canvas2"></div>
      </div>
      <div class="col-6 vh-50">
        <div id="canvas3"></div>
      </div>
      <div class="col-6 vh-50">
        <div id="canvas4"></div>
      </div>
    </div>
    <script type="module" src="/exemple/index.js"></script>
    <script
      src="https://cdn.jsdelivr.net/npm/bootstrap@5.0.1/dist/js/bootstrap.bundle.min.js"
      integrity="sha384-gtEjrD/SeCtmISkJkNUaaKMoLD0//ElJ19smozuHV6z3Iehds+3Ulb9Bn9Plx0x4"
      crossorigin="anonymous"
    ></script>
  </body>
</html>
```

Script JS:

```js
import CloudViewer from "/src/CloudViewer.js";

const viewer1 = new CloudViewer("#canvas1");
const viewer2 = new CloudViewer("#canvas2");
const viewer3 = new CloudViewer("#canvas3");
const viewer4 = new CloudViewer("#canvas4");

const cloud = {
  numpts: 7,
  points: [
    {
      x: -0.07793000340461731,
      y: 0.1751600056886673,
      z: -0.04439999908208847,
    },
    {
      x: -0.06993500143289566,
      y: 0.17982999980449677,
      z: -0.05198799818754196,
    },
    {
      x: -0.06499200314283371,
      y: 0.17802000045776367,
      z: -0.05464499816298485,
    },
    {
      x: -0.06925000250339508,
      y: 0.18199999630451202,
      z: -0.05502599850296974,
    },
    {
      x: -0.07198599725961685,
      y: 0.17611999809741974,
      z: -0.0453840009868145,
    },
    {
      x: -0.06611700356006622,
      y: 0.1735299974679947,
      z: -0.04745300114154816,
    },
    {
      x: -0.0346670001745224,
      y: 0.151309996843338,
      z: -0.0007102899835444987,
    },
  ],
};

viewer1.addCloud(cloud, "Cloud A", "#0000ff");
viewer2.addCloud(cloud, "Cloud B", "#ff0000");
viewer3.addCloud(cloud, "Cloud C", "#00ff00");
viewer4.addCloud(cloud, "Cloud D", "#f0f0f0");
```

## Tipos de Dados

Formatos de dados utilizados pela classe.

### Cloud OBJ

- **numpts** - Contém o total de pontos da nuvem;
- **points** - Vetor de objetos que representam os pontos, as propriedades desse objeto respresentam as cordenadas **x**, **y** e **z** do ponto.

Exemplo:

```js
const cloudObj = {
  numpts: 3,
  points: [
    {
      x: 0.044211581349372864,
      y: -0.02174988202750683,
      z: 0.05041627958416939,
    },
    {
      x: 0.05305223912000656,
      y: -0.02392994426190853,
      z: 0.05167124792933464,
    },
    {
      x: 0.05364399775862694,
      y: -0.023770984262228012,
      z: 0.05163086578249931,
    },
  ],
};
```
