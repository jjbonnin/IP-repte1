# MD2.1 Començam a picar codi: la nostra primera calculadora

*Guia per a l'alumnat. Primera lliçó de programació.*

---

## 0. Què farem avui?

Avui escriurem el nostre primer programa de veritat: una **calculadora**. L'usuari escriurà una operació com `3.5 * 2` i el programa la resoldrà i mostrarà el resultat a la pàgina.

No cal saber res de programació. Anirem pas a pas i cada concepte s'explicarà **abans** de fer-lo servir.

**Al final de la lliçó sabràs:**

- què és un programa i què és un llenguatge de programació;
- què és una variable i com es guarda informació;
- com demanar dades a l'usuari i com mostrar resultats;
- com fer que el programa prengui decisions;
- com controlar els errors.

---

## 1. Idees bàsiques

### Què és un programa?

Un **programa** és una llista d'instruccions que l'ordinador executa **una darrere l'altra, de dalt a baix**. Com una recepta de cuina: *primer fes això, després allò, i al final això altre*.

L'ordinador és molt obedient però **no pensa per ell mateix**: fa exactament el que li dius, ni més ni menys. Si et descuides una coma, no ho entendrà.

### Què és JavaScript?

L'ordinador no entén català ni castellà. Entén **llenguatges de programació**. **JavaScript** és el llenguatge que fan servir els navegadors (Chrome, Firefox, Edge...) per donar vida a les pàgines web.

### Què és el codi?

El **codi** és el text que escrivim en un llenguatge de programació. "Picar codi" vol dir escriure'l.

### HTML i JavaScript, qui fa què?

- **HTML** descriu **què hi ha** a la pàgina: títols, paràgrafs, botons.
- **JavaScript** descriu **què fa** la pàgina: què passa quan fas clic, com es calcula un resultat...

Ambdós viuen en **fitxers** diferents. El fitxer HTML crida el fitxer JavaScript.

---

## 2. Preparam l'entorn de proves

Crea una carpeta amb dos fitxers:

```
/prova-js/
│
├── index.html
└── script.js
```

### El fitxer `index.html`

```html
<!DOCTYPE html>
<html lang="ca">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Prova de JavaScript</title>
</head>
<body>
  <h1>Prova de codi JavaScript</h1>
  <p id="missatge">Fes clic al botó per executar el codi.</p>

  <button id="boto">Executa JS</button>

  <!-- Enllaç al fitxer extern -->
  <script src="script.js"></script>
</body>
</html>
```

Fixa't en tres coses:

- El paràgraf té un **`id="missatge"`** i el botó té **`id="boto"`**. Un `id` és un **nom** que posam a un element perquè JavaScript el pugui trobar.
- La línia `<script src="script.js">` és la que **connecta** l'HTML amb el nostre JavaScript.
- Està **al final** del `<body>` a propòsit: així, quan JavaScript s'executa, el botó i el paràgraf ja existeixen.

### El fitxer `script.js`

Crea'l **buit**. Hi escriurem tot el codi a partir d'ara.

### Com es prova?

1. Guarda els dos fitxers.
2. Obre `index.html` fent doble clic (s'obrirà al navegador).
3. Cada vegada que canviïs `script.js`, **guarda** i **actualitza** la pàgina (tecla `F5`).
4. Per veure la **consola** (on el programa escriu missatges), prem `F12` i tria la pestanya **Consola**.

---

## 3. Primer concepte: la consola

Escriu això a `script.js`, guarda i actualitza la pàgina:

```js
console.log("Hola, món!");
```

Obre la consola (`F12`). Hi veuràs `Hola, món!`.

- **`console.log(...)`** és una **instrucció** que escriu un missatge a la consola. És la "pantalla" del programador, i la utilitzarem molt per comprovar què fa el nostre programa.
- El que va **entre parèntesis** és el que volem mostrar.
- El text va **entre cometes**. Un text s'anomena **cadena** (en anglès, *string*).
- El **punt i coma** `;` al final marca que la instrucció s'ha acabat.

> **Prova-ho tu:** canvia el text per un altre i comprova que surt a la consola.

---

## 4. Segon concepte: les variables

Una **variable** és una **caixa amb nom** on es guarda una dada perquè la puguem fer servir després.

```js
let nom = "Maria";
console.log(nom);
```

Això vol dir:

1. **`const`**: "crea una caixa nova".
2. **`nom`**: "la caixa es diu *nom*" (aquest nom el triam nosaltres).
3. **`=`**: "guarda a dins". **No vol dir "és igual"** com a matemàtiques: vol dir "posa aquest valor a la caixa".
4. **`"Maria"`**: la dada que guardam.

Quan escrivim `console.log(nom)` **sense cometes**, JavaScript no mostra la paraula "nom", sinó **el que hi ha dins la caixa**: `Maria`.

```js
console.log("nom");   // mostra: nom   (el text)
console.log(nom);     // mostra: Maria (el contingut de la caixa)
```

> **Comentaris:** tot el que va després de `//` és un comentari. L'ordinador l'ignora. Serveix perquè nosaltres deixem notes al codi.

### `const` i `let`

Hi ha dues maneres de crear una caixa:

| Paraula | Quan s'utilitza |
| --- | --- |
| `const` | El valor **no canviarà** mai |
| `let` | El valor **pot canviar** més endavant |

```js
let punts = 0;      // comença a 0
punts = 10;         // ara val 10 (no cal tornar a escriure let)
```

Si intentes canviar una variable creada amb `const`, el programa dóna error.

### Normes per posar nom a una variable

- Sense espais: `primer_nombre` o `primerNombre`, mai `primer nombre`.
- No pot començar per un número.
- Ha de ser **descriptiu**: `resultat` és millor que `x`.
- Majúscules i minúscules **són diferents**: `Nom` i `nom` són dues caixes distintes.

---

## 5. Tercer concepte: tipus de dades

A les caixes hi podem guardar diferents **tipus** de dades. De moment en necessitam dos:

| Tipus | Exemple | Com s'escriu |
| --- | --- | --- |
| **Text** (cadena) | `Hola` | Amb cometes: `"Hola"` |
| **Nombre** | `3.5` | Sense cometes: `3.5` |

**Atenció:** els decimals s'escriuen **amb punt**, no amb coma: `3.5`, no `3,5`.

Hi ha una diferència molt important entre `3` i `"3"`:

```js
console.log(3 + 4);      // 7     (suma de nombres)
console.log("3" + "4");  // 34    (uneix textos!)
```

Amb nombres, `+` **suma**. Amb textos, `+` **uneix**. Això és important, perquè el que escriu l'usuari **sempre arriba com a text**, i l'haurem de convertir en nombre.

### Operadors matemàtics

| Símbol | Operació | Exemple | Resultat |
| --- | --- | --- | --- |
| `+` | Suma | `7 + 3` | `10` |
| `-` | Resta | `7 - 3` | `4` |
| `*` | Multiplicació | `7 * 3` | `21` |
| `/` | Divisió | `7 / 2` | `3.5` |
| `%` | Mòdul (el **residu** d'una divisió) | `7 % 3` | `1` |

El **mòdul** és el que sobra: 7 entre 3 hi cap 2 vegades (que fan 6) i **sobra 1**.

---

## 6. Quart concepte: demanar dades amb `prompt`

```js
const entrada = prompt("Escriu una operació, per exemple 3.5 * 2");
console.log("Has escrit: " + entrada);
```

- **`prompt("text")`** obri una finestreta amb la pregunta i un espai per escriure.
- El que l'usuari escriu **es guarda a la variable** `entrada` (gràcies al `=`).
- Després l'utilitzam a `console.log`. Aquí el `+` **uneix** el text `"Has escrit: "` amb el contingut de `entrada`.

**Si l'usuari prem *Cancel·lar***, `prompt` retorna un valor especial anomenat **`null`**, que vol dir "res". Ho haurem de controlar.

---

## 7. Cinquè concepte: prendre decisions amb `if`

Un programa útil ha de poder **decidir**. Per això tenim `if` ("si"):

```js
const edat = 17;

if (edat >= 18) {
  console.log("Ets major d'edat");
} else {
  console.log("Ets menor d'edat");
}
```

- **`if (condició)`**: "si això és cert..."
- Entre **claus `{ }`** va el codi que s'executa si la condició és certa.
- **`else`**: "si no..."
- Si hi ha més d'una possibilitat, s'afegeix **`else if`**:

```js
if (edat < 12) {
  console.log("Infant");
} else if (edat < 18) {
  console.log("Adolescent");
} else {
  console.log("Adult");
}
```

JavaScript prova les condicions **de dalt a baix** i executa **només el primer bloc** que sigui cert.

### Operadors de comparació

| Símbol | Significa |
| --- | --- |
| `==` | és igual a |
| `!=` | és diferent de |
| `>` / `<` | major que / menor que |
| `>=` / `<=` | major o igual / menor o igual |

> **Compte!** Un sol `=` **guarda** un valor (`const x = 5`). Tres `===` **comparen** (`x === 5`). És l'error més habitual de qui comença.

---

## 8. Sisè concepte: les funcions

Una **funció** és un bloc de codi **amb nom** que només s'executa quan **el cridam**. És com una recepta guardada al llibre: no es cuina fins que decidim fer-la.

```js
function saludar() {
  console.log("Hola!");
}

saludar();   // aquí s'executa
saludar();   // i aquí un altre cop
```

- **`function`**: "definesc una funció".
- **`saludar`**: el nom que li posam.
- **`()`**: els parèntesis són obligatoris. Quan **cridam** la funció, escrivim el nom **amb parèntesis**: `saludar()`.
- Entre **`{ }`** hi va el codi que executa.

A JavaScript ja hi ha funcions fetes que hem vist: `console.log(...)` i `prompt(...)` són funcions. Els valors que posam entre parèntesis s'anomenen **arguments**.

---

## 9. Setè concepte: connectar el botó amb la pàgina

Ara anam a connectar el JavaScript amb l'HTML.

```js
const missatge = document.getElementById("missatge");
const boto = document.getElementById("boto");
```

- **`document`** representa la pàgina HTML sencera.
- **`getElementById("boto")`** vol dir: "cerca a la pàgina l'element que té `id="boto"`".
- El resultat es guarda en una variable, i així podem manipular el botó i el paràgraf des de JavaScript.

Per **canviar el text** del paràgraf:

```js
missatge.textContent = "Hola des de JavaScript!";
```

I per **reaccionar a un clic**:

```js
function saludar() {
  missatge.textContent = "Has fet clic!";
}

boto.addEventListener("click", saludar);
```

`addEventListener` significa "escolta". Aquesta línia diu: *"quan es faci un **clic** al botó, executa la funció `saludar`"*.

**Fixa't:** escrivim `saludar` **sense parèntesis**. No volem executar-la ara, sinó dir-li al botó **quina funció** ha d'executar quan el cliquin. Si escrivíssim `saludar()`, s'executaria immediatament en carregar la pàgina.

> **Prova-ho tu:** copia aquest codi, fes clic al botó i comprova que el paràgraf canvia.

---

## 10. Vuitè concepte: les expressions regulars

Volem que l'usuari escrigui `3.5 * 2` i que el programa **entengui** les tres parts: `3.5`, `*` i `2`. Per fer-ho necessitam dues coses: comprovar que el text té **aquesta forma** i **separar-ne** les parts.

Una **expressió regular** és un **motlle** que descriu com ha de ser un text. Va entre barres `/ ... /`.

```js
const patro = /^\s*(-?\d+(?:\.\d+)?)\s*([+\-*/%])\s*(-?\d+(?:\.\d+)?)\s*$/;
```

Pareix criptogràfic, però es llegeix **per peces**:

| Peça | Significa |
| --- | --- |
| `^` | El text **comença** aquí |
| `\s*` | Zero o més **espais** (així admet `3+4` i `3 + 4`) |
| `\d` | Un **dígit** (0 a 9) |
| `\d+` | **Un o més** dígits (`7`, `42`, `305`) |
| `\.` | Un punt **de veritat** (sense la barra, `.` voldria dir "qualsevol caràcter") |
| `(?:\.\d+)?` | **Opcional** (pel `?` final): un punt i més dígits |
| `[+\-*/%]` | **Un** caràcter d'aquesta llista: `+ - * / %` |
| `$` | El text **acaba** aquí |

Així, un **nombre** és `-?\d+(?:\.\d+)?`. El `-?` vol dir "un signe menys, però **opcional**": per això accepta `3`, `3.14` i també negatius com `-5` o `-2.5`. Continua sense admetre `.5` ni `5.`.

El motlle complet diu:

> espais, **nombre**, espais, **operador**, espais, **nombre**, espais

Els **parèntesis normals** `( )` marquen les tres parts que volem recuperar. Són els "calaixos" on JavaScript guardarà el primer nombre, l'operador i el segon nombre.

### Dividir el text amb `match`

```js
const parts = "3.5 * 2".match(patro);
```

`match` compara el text amb el motlle:

- Si **encaixa**, retorna una **llista** (en diem *array*) amb les parts.
- Si **no encaixa**, retorna `null`.

```js
parts[0]   // "3.5 * 2"  (tot el text)
parts[1]   // "3.5"      (primer nombre)
parts[2]   // "*"        (operador)
parts[3]   // "2"        (segon nombre)
```

Una **llista** és una col·lecció de dades ordenada. Cada element té una **posició** que es compta **començant per 0**, i es demana amb **claudàtors**: `parts[1]`.

### Convertir text en nombre

`parts[1]` és el **text** `"3.5"`, no el nombre 3.5. Per fer càlculs l'hem de convertir amb **`parseFloat`**:

```js
const nombre1 = parseFloat(parts[1]);   // el nombre 3.5
```

---

## 11. Novè concepte: errors amb `throw` i `try / catch`

Quan alguna cosa va malament (l'usuari escriu "hola" en lloc d'una operació, o intenta dividir entre zero), el programa **no pot continuar**. Hem de saber:

1. **Avisar** que hi ha un problema → `throw`
2. **Reaccionar** al problema → `try / catch`

### `throw`: llançar un error

```js
throw new Error("Alguna cosa ha anat malament");
```

`throw` ("llançar") atura el programa en aquell punt i **dispara una alarma**, amb un missatge que explica què ha passat. Hi ha diferents tipus d'error: `Error` (general), `SyntaxError` (format incorrecte), `RangeError` (valor fora de límits).

### `try / catch`: atrapar l'error

```js
try {
  // codi que pot fallar
} catch (error) {
  // què fem si falla
}
```

- Dins del **`try`** ("intenta") hi va el codi que pot fallar.
- Si algun `throw` es dispara, JavaScript **salta directament** al `catch` ("atrapa"), **sense executar** la resta del `try`.
- **`error`** és una variable que conté l'error atrapat, i **`error.message`** és el seu missatge.

Sense `try/catch`, un error fa que el programa es trenqui amb un missatge lleig. Amb ell, mostram un avís clar i el programa continua funcionant.

```js
try {
  console.log("Abans");
  throw new Error("Ostres!");
  console.log("Això no es mostrarà mai");
} catch (error) {
  console.log("Error: " + error.message);
}
```

El resultat és `Abans` i després `Error: Ostres!`. La línia del mig **no s'executa**.

> **Per què controlam la divisió entre zero a mà?** Perquè JavaScript **no dóna error**: retorna `Infinity` o `NaN`, que confonen a qui comença. És més clar avisar amb un missatge.

---

## 12. Ho ajuntam tot: la calculadora completa

Ara tens totes les peces. Copia aquest codi a `script.js`, **llegeix els comentaris** i comprova que entens cada part.

```js
// 1. AGAFAM ELS ELEMENTS DE LA PÀGINA
// getElementById cerca a l'HTML l'element que té aquest id
// i el guardam en una variable per poder-lo utilitzar.
const missatge = document.getElementById("missatge");
const boto = document.getElementById("boto");

// 2. EL MOTLLE (expressió regular)
// Descriu com ha de ser el text: nombre, operador, nombre (els nombres poden ser negatius).
const patro = /^\s*(-?\d+(?:\.\d+)?)\s*([+\-*/%])\s*(-?\d+(?:\.\d+)?)\s*$/;

// 3. LA FUNCIÓ QUE FA EL CÀLCUL
// Una funció és un bloc de codi amb nom que només s'executa quan la cridam.
function calcular() {
  try {
    // 3.1 Demanar l'operació
    const entrada = prompt("Escriu una operació, per exemple 3.5 * 2");

    // Si l'usuari prem Cancel·lar, prompt retorna null
    if (entrada === null) {
      throw new Error("Has cancel·lat l'operació");
    }

    // 3.2 Dividir l'entrada en parts
    const parts = entrada.match(patro);

    if (parts === null) {
      throw new SyntaxError("L'expressió no és vàlida. Usa: nombre operador nombre");
    }

    // 3.3 Guardar cada part en una variable (i convertir el text en nombre)
    const nombre1 = parseFloat(parts[1]);
    const operador = parts[2];
    const nombre2 = parseFloat(parts[3]);

    // 3.4 Calcular segons l'operador
    let resultat;

    if (operador === "+") {
      resultat = nombre1 + nombre2;
    } else if (operador === "-") {
      resultat = nombre1 - nombre2;
    } else if (operador === "*") {
      resultat = nombre1 * nombre2;
    } else if (operador === "/") {
      if (nombre2 === 0) {
        throw new RangeError("No es pot dividir entre zero");
      }
      resultat = nombre1 / nombre2;
    } else if (operador === "%") {
      if (nombre2 === 0) {
        throw new RangeError("No es pot calcular el mòdul entre zero");
      }
      resultat = nombre1 % nombre2;
    }

    // 3.5 Mostrar el resultat (a la consola i a la pàgina)
    const text = nombre1 + " " + operador + " " + nombre2 + " = " + resultat;
    console.log(text);
    missatge.textContent = text;

  } catch (error) {
    // Qualsevol throw de dalt acaba aquí
    console.log("Error: " + error.message);
    missatge.textContent = "Error: " + error.message;
  }
}

// 4. CONNECTAR EL BOTÓ AMB LA FUNCIÓ
// "Quan es faci clic al botó, executa calcular"
boto.addEventListener("click", calcular);
```

### Què passa quan faig clic? (el recorregut)

Per a l'entrada `3.5 * 2`:

1. Es fa clic al botó → s'executa `calcular`.
2. `prompt` demana l'operació → `entrada` guarda `"3.5 * 2"`.
3. `match` divideix el text → `parts` és `["3.5 * 2", "3.5", "*", "2"]`.
4. `parseFloat` converteix → `nombre1` val `3.5`, `operador` val `"*"`, `nombre2` val `2`.
5. Els `if / else if` troben que l'operador és `"*"` → `resultat` val `7`.
6. Es mostra `3.5 * 2 = 7` a la consola i al paràgraf.

Si **qualsevol pas falla** (`throw`), el programa salta al `catch` i mostra l'error.

---

## 13. Taula de proves

Feis clic al botó, escriviu l'entrada i comprovau que el resultat coincideix.

| Entrada | Resultat a la pàgina |
| --- | --- |
| `7 + 3` | `7 + 3 = 10` |
| `3.5*2` | `3.5 * 2 = 7` |
| `10 - 4` | `10 - 4 = 6` |
| `9 / 2` | `9 / 2 = 4.5` |
| `10 % 3` | `10 % 3 = 1` |
| `-5 + 2` | `-5 + 2 = -3` |
| `4 * -3` | `4 * -3 = -12` |
| `5 - -3` | `5 - -3 = 8` |
| `-7 % 3` | `-7 % 3 = -1` |
| `8 / 0` | `Error: No es pot dividir entre zero` |
| `8 % 0` | `Error: No es pot calcular el mòdul entre zero` |
| `1 + 2 + 3` | `Error: L'expressió no és vàlida...` |
| `hola` | `Error: L'expressió no és vàlida...` |
| `.5 + 1` | `Error: L'expressió no és vàlida...` |
| *(Cancel·lar)* | `Error: Has cancel·lat l'operació` |

**Pregunta per pensar:** `-7 % 3` dóna `-1`, no `2`. De quin dels dos nombres agafa el signe el residu?

---

## 14. Errors típics de principiants

| Què passa | Probable causa |
| --- | --- |
| No passa res en fer clic | No has guardat `script.js` o no has actualitzat la pàgina (`F5`) |
| La consola diu `... is not defined` | Hi ha una errada d'escriptura al nom d'una variable (recorda: majúscules i minúscules importen) |
| La consola diu `Cannot read properties of null` | El `id` de l'HTML no coincideix amb el que has escrit a `getElementById` |
| La consola diu `Unexpected token` | Falta o sobra un parèntesi, una clau `}` o unes cometes |
| El resultat és `34` en comptes de `7` | Estàs unint **textos** en lloc de sumar nombres (falta `parseFloat`) |

**Consell:** quan alguna cosa no funciona, **obre la consola (`F12`)**. Normalment indica la línia on hi ha el problema.

---

## 15. Exercicis

### Nivell 1: Tocar el codi existent

1. **Missatges propis.** Canvia els missatges d'error per uns altres que t'agradin més.
2. **Canviar el prompt.** Modifica la pregunta perquè digui: "Quina operació vols calcular?".
3. **Canviar l'HTML.** Fes que el botó es digui "Calcula" i que el paràgraf inicial doni instruccions.

### Nivell 2: Ampliar la calculadora

4. **Nombres negatius: com funcionen?** Al motlle, el `-?` vol dir "un signe menys, però opcional". Treu-lo (les dues vegades) i prova `-5 + 2`: què passa? Torna'l a posar. *Pista:* prova també `5 - -3`.
5. **Arrodonir.** Prova `0.1 + 0.2`. Què passa? Cerca què fa `toFixed(2)` i aplica'l al resultat.
6. **Nou operador: potència.** Afegeix `**` perquè `2 ** 3` doni `8`. Hauràs de modificar la regex i afegir un `else if`.

### Nivell 3: Investigar

7. **Error en vermell.** Dins del `catch`, afegeix `missatge.style.color = "red";`. Quan es torna a posar en negre? Soluciona-ho.
8. **Repetir fins que sigui vàlid.** Investiga el bucle `while` perquè, si l'entrada no és vàlida, el programa torni a preguntar.
9. **Historial.** Guarda cada resultat en una llista amb `push` i mostra'ls tots a la consola.

---

## 16. Glossari

| Terme | Significat |
| --- | --- |
| **Programa** | Llista d'instruccions que l'ordinador executa de dalt a baix |
| **Codi** | El text que escrivim en un llenguatge de programació |
| **Variable** | Caixa amb nom on es guarda una dada |
| **`const` / `let`** | Maneres de crear una variable (que no canvia / que pot canviar) |
| **Cadena (string)** | Un text entre cometes |
| **Nombre** | Una dada numèrica, sense cometes |
| **`console.log`** | Instrucció que escriu un missatge a la consola |
| **`prompt`** | Funció que demana una dada a l'usuari |
| **`null`** | Valor que significa "res" |
| **Condició (`if`)** | Permet que el programa prengui decisions |
| **Funció** | Bloc de codi amb nom que s'executa quan el cridam |
| **Argument** | Valor que passam a una funció entre parèntesis |
| **Llista (array)** | Col·lecció ordenada de dades; es numera des de 0 |
| **Expressió regular** | Motlle que descriu com ha de ser un text |
| **`match`** | Compara un text amb un motlle i el divideix en parts |
| **`parseFloat`** | Converteix un text en un nombre amb decimals |
| **`throw`** | Llança un error i atura el programa en aquell punt |
| **`try / catch`** | Intenta executar codi i, si hi ha error, el captura |
| **Esdeveniment** | Una cosa que passa a la pàgina (per exemple, un clic) |
| **`addEventListener`** | Connecta un esdeveniment amb una funció |
