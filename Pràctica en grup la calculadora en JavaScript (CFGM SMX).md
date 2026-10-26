# Repte 1. Calculadora

*Pràctica en grup: construïm una calculadora en JavaScript · Iniciació a la Programació en JavaScript · CFGM SMX*

---

## 1. Presentació

Cada grup construeix una **calculadora que funciona al navegador** (`+ - * / %`). L'usuari escriu una operació com `3.5 * 2` i el programa la resol i mostra el resultat a la pàgina.

La calculadora ha de:

- demanar l'operació amb un `prompt`;
- dividir-la en tres parts (nombre, operador, nombre) i comprovar que és vàlida;
- controlar els errors amb `throw` i `try / catch`;
- escriure **missatges de log** a la consola, que s'**activen o desactiven** canviant una sola línia;
- portar una **bateria de proves** automàtica, que també s'**activa o desactiva** canviant una sola línia.

> **Abast del Repte 1. Només fem servir variables, tipus bàsics, operadors, condicionals, **funcions** i la llista que retorna `match` (només per llegir-la). Utilitzam objectes que ja vénen fets (`console`, `document`), però no en creem cap.

### Què es treballa

- Dividir un programa en **funcions petites**, cada una amb una tasca concreta.
- Escriure funcions amb paràmetres i valor de retorn (`return`).
- Convertir text en nombres per fer càlculs.
- Prendre decisions amb `if / else if / else`.
- Validar i dividir un text amb una expressió regular.
- Llançar i capturar errors amb `throw` i `try / catch`.
- Connectar JavaScript amb una pàgina HTML.
- Depurar amb missatges de log i **verificar** amb proves.
- Treballar en equip

### Durada i format

- Temps estimat entre 2 i 3 setmanes (dues sessions per setmana).
- Sessions d'una hora.
- Grups de **3 o 4** alumnes.
- Material: ordinador amb navegador (Chrome, Firefox o Edge) i un editor de text (Visual Studio Code, Sublime Text, Notepad++...).
- **La teoria no es repeteix aquí:** l'alumnat ja té els apunts. La secció 5 és un **recopilatori** del que cal haver vist per poder fer la calculadora.

---

## 2. Organització: responsable i verificador

Al Repte 1 **no hi ha rols fixos** (Cap de Projecte, Responsable de seguiment, etc).

1. Ser **responsable** d'unes quantes funcions petites: les dissenya, les programa i les defensa.
2. Ser **verificador** de les funcions d'un company: dissenya el **pla de proves** que demostra que funcionen.

Així, tothom escriu codi **i** el posa a prova, i ningú verifica el seu propi codi.

### Unitats de codi

Una **unitat de codi** és una peça petita del programa amb una sola feina. Segons el llenguatge rep noms diferents; això és el que fem servir al Repte 1:

| Nom | Què és | Al Repte 1 |
| --- | --- | --- |
| **Funció** | Bloc amb nom que rep dades i retorna un valor | **Sí:** les unitats són funcions |
| **Subrutina** | Bloc que fa una acció i no retorna res | **Sí:** una funció sense `return` (p. ex. `log`) |
| **Mòdul** | Un fitxer amb funcions relacionades | **Sí:** un fitxer `.js` per responsable |
| **Paquet** | Conjunt de mòduls | **Sí:** la carpeta del projecte |
| **Interfície** | El que una unitat ofereix i espera dels altres | **Sí:** el **requeriment** escrit |
| **Mètode, classe, espai de noms** | Funcions i dades agrupades en objectes | **No:** es deixen per quan es treballin els objectes |

### Regles per fer unitats ben fetes

1. **Una funció, una feina.** Si per explicar què fa cal dir «i», probablement són dues funcions.
2. **Petites:** de 5 a 15 línies.
3. **Amb requeriment:** nom, paràmetres, valor que retorna i errors que llança.
4. **Les funcions de càlcul no toquen la pàgina ni demanen dades:** reben valors i retornen un valor.
5. **Les funcions llancen els errors i només un lloc els captura** (`alPremerBoto`), perquè és l'únic que pot avisar l'usuari.
6. **Les dades viatgen per paràmetres i amb `return`.** No es comparteixen variables entre fitxers, tret de les constants de configuració i els comptadors de proves.
7. **Noms descriptius** en català, sense espais ni accents: `validarEntrada`, `obtenirNombre1`.

### Mapa del programa

Qui crida qui (el fitxer on viu cada funció, a la dreta):

```
alPremerBoto()                            pagina.js
 ├─ calcular(entrada)                     calculadora.js
 │   ├─ validarEntrada(entrada)           entrada.js
 │   ├─ obtenirNombre1(text)              entrada.js
 │   ├─ obtenirOperador(text)             entrada.js
 │   ├─ obtenirNombre2(text)              entrada.js
 │   └─ operar(nombre1, operador, nombre2)  calculadora.js
 │       ├─ sumar, restar, multiplicar    aritmetica.js
 │       └─ dividir, modul                aritmetica.js
 └─ mostrarMissatge(text)                 pagina.js
```

Per deixar missatges a la consola, `log(text)` (a `log.js`) es pot cridar des de qualsevol funció.

### Unitats i responsables

| Unitat | Fitxer | Funcions | Grup de 4 | Grup de 3 |
| --- | --- | --- | --- | --- |
| **U1** Entrada | `entrada.js` | `validarEntrada`, `obtenirNombre1`, `obtenirOperador`, `obtenirNombre2` | A | A, més `eines-proves.js` |
| **U2** Aritmètica | `aritmetica.js` | `sumar`, `restar`, `multiplicar`, `dividir`, `modul` | B, més `log.js` | B, més `log.js` |
| **U3** Càlcul | `calculadora.js` | `operar`, `calcular` | C | C, més U4 |
| **U4** Pàgina | `pagina.js` | `mostrarMissatge`, `alPremerBoto` | D, més `eines-proves.js` | (la fa C) |

### Qui verifica qui

Es forma una cadena perquè ningú verifiqui la seva pròpia unitat:

| Unitat | Responsable | Verificador (grup de 4) | Verificador (grup de 3) |
| --- | --- | --- | --- |
| U1 | A | B | B |
| U2 | B | C | C |
| U3 | C | D | A |
| U4 | D | A | A |

Els fitxers de suport (`log.js` i `eines-proves.js`) els verifica el mateix verificador de la unitat del seu responsable.

### El requeriment de cada funció

Abans de programar, el responsable completa la **fitxa de requeriment** de cada funció: la promesa que fa a les altres. Sense requeriment, les unitats no encaixen. El verificador **només necessita el requeriment** per dissenyar les proves; no cal que miri el codi.

| Camp | Què s'hi escriu |
| --- | --- |
| Nom | El nom exacte de la funció (les altres la cridaran així) |
| Fitxer | On viu (`aritmetica.js`) |
| Què fa | Una frase |
| Paràmetres | Nom, tipus i què representa cada un |
| Condicions prèvies | Què ha de complir l'entrada perquè la funció funcioni |
| Retorna | Tipus i què representa (o «res») |
| Errors | Quin tipus d'error llança i quan |
| Exemples | Almenys 3 casos: entrada → sortida |


### Cicle de treball de cada unitat

1. **Requeriment.** El responsable completa la fitxa de cada funció.
2. **Pla de proves.** El verificador, **sense mirar el codi**, dissenya una taula de proves a partir del requeriment.
3. **Programació.** El responsable escriu les funcions.
4. **Execució.** El verificador converteix el pla en codi, l'executa i anota el resultat de cada prova.
5. **Informe d'errors.** Per cada prova fallida, escriu l'entrada, l'esperat i l'obtingut.
6. **Correcció.** El responsable corregeix i es torna al pas 4, fins que tot passi.
7. **Integració.** Quan totes les unitats passen, el grup les uneix i fa proves d'integració.

### Plantilla del pla de proves

| ID | Funció | Descripció | Tipus | Entrada | Resultat esperat | Obtingut | OK? |
| --- | --- | --- | --- | --- | --- | --- | --- |
| A1 | `sumar` | Suma de dos enters | Normal | `7`, `3` | `10` |  |  |

Tipus: **normal** (cas habitual), **límit** (zero, negatius, decimals, espais) i **invàlid** (ha de llançar un error). Mínim **5 proves** per unitat, amb almenys una de cada tipus.

### Plantilla d'informe d'errors

| ID de la prova | Entrada | Esperat | Obtingut | Observacions |
| --- | --- | --- | --- | --- |
|  |  |  |  |  |

### Normes de treball

1. Cada responsable escriu només en **els seus fitxers**.
2. El verificador **no corregeix** el codi: informa de l'error i el responsable el corregeix.
3. El requeriment només es canvia amb l'acord del responsable i del verificador.
4. Tothom ha d'entendre tot el codi: a la defensa final el professor pot preguntar qualsevol línia a qualsevol alumne.
5. El treball es desa al final de cada sessió en la carpeta `calculadora-grupX`.

---

## 3. Planificació

### Opció A: 3 setmanes (6 sessions)

Les **B1–B11** són els blocs del recopilatori de teoria (secció 5): l'alumnat ja els té als seus apunts i només cal comprovar que els ha vist.

| Sessió | Teoria | Treball del grup | Lliurable |
| --- | --- | --- | --- |
| **S1** | B1–B4 | Formar els grups, repartir **unitats i verificadors**, crear la carpeta i els fitxers buits. Cada responsable llegeix el requeriment de les seves funcions i el completa amb exemples. | Fitxes de requeriment completades |
| **S2** | B5–B7, B11 | Cada verificador dissenya el **pla de proves en taula** a partir del requeriment, sense veure el codi. Cada responsable comença les funcions (versió 1, sense errors). Qui té `log.js` i `eines-proves.js` els acaba aquesta sessió. | Pla de proves en taula, `log.js` i `eines-proves.js` |
| **S3** | B8, B9 | Els responsables acaben la versió 1 (regex, `throw`). Els verificadors **converteixen el pla en codi** (`proves-*.js`) amb les eines de proves. | Funcions v1 i pla de proves en codi |
| **S4** | B10 | Es programa la pàgina (U4). Els verificadors executen els plans i redacten l'informe d'errors; els responsables corregeixen, fins que tot passi. | Unitats que passen el seu pla, i informes d'errors |
| **S5** | — | **Integració:** `index.html`, `principal.js` i interruptors de log i proves. Proves d'integració de `calcular`. | Calculadora completa |
| **S6** | — | Revisió creuada entre grups, ampliacions i defensa. | Projecte final, diari de grup i defensa |

### Opció B: 2 setmanes (4 sessions)

| Sessió | Teoria | Treball del grup | Lliurable |
| --- | --- | --- | --- |
| **S1** | B1–B7 (repàs ràpid) | Repartiment d'unitats i verificadors. Fitxes de requeriment. | Requeriments completats |
| **S2** | B8, B9, B11 | Els responsables programen; els verificadors dissenyen el pla de proves i el converteixen en codi. | Funcions v1 i plans de proves |
| **S3** | B10 | Pàgina (U4), execució dels plans, informes d'errors i correccions. | Unitats que passen el seu pla |
| **S4** | — | Integració, interruptors, revisió i defensa. | Projecte final i defensa |

**Recomanacions per a l'opció B:**

- Demana a l'alumnat que **repassi els apunts abans de cada sessió**, amb el recopilatori a la mà.
- Dona a cada responsable un **esquelet** dels seus fitxers: les funcions buides, el requeriment com a comentari i `// TODO`.
- Redueix el pla de proves a 5 casos per unitat i deixa de banda les ampliacions.

### Diari de grup (plantilla)

Cada grup l'omple al final de cada sessió, entre tots.

| Sessió | Unitat (responsable / verificador) | Què hem fet | Errors trobats i com els hem resolt | Què falta |
| --- | --- | --- | --- | --- |
| S1 |  |  |  |  |

---

## 4. Preparació de l'entorn

Cada mòdul (fitxer) té un responsable i així cada alumne treballa al seu sense trepitjar els altres. **Creeu tots els fitxers buits el primer dia.**

```
/calculadora-grupX/
│
├── index.html
├── config.js                   interruptors (tot el grup, a la S5)
├── log.js                      log                 (B)
├── eines-proves.js             eines de proves     (D; A al grup de 3)
├── entrada.js                  U1                  (A)
├── aritmetica.js               U2                  (B)
├── calculadora.js              U3                  (C)
├── pagina.js                   U4                  (D; C al grup de 3)
├── proves-entrada.js           pla de proves de U1 (verificador de U1)
├── proves-aritmetica.js        pla de proves de U2
├── proves-calculadora.js       pla de proves de U3
└── principal.js                arrencada (tot el grup, a la S5)
```

**`index.html`:**

```html
<!DOCTYPE html>
<html lang="ca">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Calculadora</title>
</head>
<body>
  <h1>Calculadora</h1>
  <p id="missatge">Fes clic al botó per fer una operació.</p>

  <button id="boto">Calcula</button>

  <!-- L'ORDRE IMPORTA: primer les funcions i, al final, principal.js -->
  <script src="config.js"></script>
  <script src="log.js"></script>
  <script src="eines-proves.js"></script>
  <script src="entrada.js"></script>
  <script src="aritmetica.js"></script>
  <script src="calculadora.js"></script>
  <script src="pagina.js"></script>
  <script src="proves-entrada.js"></script>
  <script src="proves-aritmetica.js"></script>
  <script src="proves-calculadora.js"></script>
  <script src="principal.js"></script>
</body>
</html>
```

- `id="missatge"` i `id="boto"` són **noms** perquè JavaScript pugui trobar els elements.
- Els `<script>` van **al final** del `<body>`, **en aquest ordre**. `principal.js` va l'últim perquè, quan s'executa, tot ho ha de trobar ja carregat.
- Tots els fitxers comparteixen els mateixos noms, com si fossin un de sol: **no repetiu el nom** d'una funció o constant entre fitxers.
- Cada vegada que canviïu un fitxer: **guardau** i **actualitzau** la pàgina (`F5`).
- La **consola** s'obre amb `F12` → pestanya *Consola*.

---

## 5. Recopilatori de teoria

Això **no és teoria nova**: l'alumnat ja té els apunts. És la llista del que cal **haver vist** per fer la calculadora, amb la sintaxi exacta que apareix al codi. Serveix per comprovar, abans de cada sessió, que no falta res. Entre parèntesis, les unitats que ho necessiten.

### B1. Programa, consola i comentaris *(totes)*

- Un programa és una llista d'instruccions que s'executen **de dalt a baix**.
- `console.log(valor)` escriu a la consola (`F12` → *Consola*). Es poden posar diversos valors separats per comes.
- `//` inicia un comentari; `;` tanca una instrucció.
- El codi es guarda en fitxers `.js` que l'HTML enllaça amb `<script src="fitxer.js"></script>`.

### B2. Variables *(totes)*

- Una variable és una **caixa amb nom** on es guarda una dada.
- `const nom = valor;` (el valor no canvia) i `let nom = valor;` (pot canviar). Per canviar-la després: `total = total + 1;`.
- El signe `=` **guarda**; no compara.
- Noms: sense espais ni accents, no comencen per un número, les majúscules i minúscules són diferents i han de ser descriptius (`nombre1`).
- **Àmbit:** una variable declarada dins d'una funció només existeix dins d'ella.

### B3. Tipus de dades i conversió *(U1, U3, proves)*

- Tipus: text (`"hola"`), nombre (`3.5`, decimals amb **punt**), booleà (`true` / `false`), `null` («res») i `undefined`.
- `typeof valor` diu de quin tipus és.
- Amb `+`, dos nombres se sumen (`3 + 4` és `7`) i dos textos s'**uneixen** (`"3" + "4"` és `"34"`).
- Tot el que arriba de `prompt` és **text**: s'ha de convertir amb `parseFloat("3.5")`.
- `parseFloat("hola")` dona `NaN` («no és un nombre»).

### B4. Operadors *(U2, U3, proves)*

- Aritmètics: `+  -  *  /  %`. El `%` és el **residu**: `7 % 3` és `1` i `-7 % 3` és `-1`.
- Comparació: `===  !==  <  >  <=  >=`. Es compara amb **tres** `=`.
- Lògics: `&&` (i), `||` (o) i `!` (no).

### B5. Condicionals *(U1, U2, U3)*

- `if (condició) { ... } else if (condició) { ... } else { ... }`.
- Les condicions es proven **de dalt a baix** i s'executa **només el primer bloc** que és cert.
- Una condició és una expressió que dona `true` o `false`.
- Es poden posar `if` dins d'altres blocs (p. ex. comprovar el zero dins de `dividir`).

### B6. Funcions *(totes)*

- Definició: `function nom(a, b) { ... }`. Crida: `nom(2, 3)`.
- Els **paràmetres** són les dades que rep la funció.
- `return valor;` **retorna** un valor a qui l'ha cridada i acaba la funció. Una funció **sense `return`** és una subrutina.
- Mostrar un valor amb `console.log` **no** és retornar-lo.
- El valor retornat es pot guardar: `const text = validarEntrada(entrada);`.
- Una funció pot cridar-ne d'altres (`calcular` crida `validarEntrada`, `operar`...).
- **Requeriment:** nom, paràmetres, condicions prèvies, valor retornat i errors que llança.

### B7. Entrada i sortida de dades *(U3, U4)*

- `prompt("pregunta")` retorna el que escriu l'usuari (**text**) o `null` si prem *Cancel·lar*.
- `text.trim()` treu els espais de l'inici i del final.
- Unir text i valors: `entrada + " = " + resultat`.
- La sortida va a la consola (`console.log`) o a la pàgina (B10).

### B8. Expressions regulars *(U1)*

- Un **motlle** que descriu com ha de ser un text, entre barres: `/ ... /`.
- Peces que fem servir: `^` i `$` (inici i final), `\s*` (espais), `\d+` (dígits), `-?` (menys opcional), `(?:\.\d+)?` (decimals opcionals; el punt s'escriu `\.`), `[+\-*/%]` (un operador) i `( )` (parts que es poden recuperar).
- `patro.test(text)` retorna `true` o `false`.
- `text.match(patro)` retorna una **llista** (o `null` si no encaixa). Es llegeix amb claudàtors: `parts[1]`, `parts[2]`, `parts[3]`; la posició 0 és el text sencer i **es compta des de 0**.
- **Només llegim aquesta llista; no en creem de pròpies.**

### B9. Errors *(U1, U2, U3, U4)*

- `throw new Error("missatge")` llança un error i **atura la funció**. Tipus: `Error`, `SyntaxError`, `RangeError`.
- `try { ... } catch (error) { ... }`: si dins del `try` hi ha un `throw`, JavaScript **salta al `catch`**.
- `error.name` és el tipus de l'error i `error.message`, el seu text.
- JavaScript **no** dona error en dividir entre zero (retorna `Infinity` o `NaN`): ho hem de controlar nosaltres.
- Regla del Repte 1: les funcions **llancen** els errors i hi ha **un sol** `try / catch` al programa (`alPremerBoto`), a part dels de les proves.

### B10. La pàgina web *(U4)*

- `document.getElementById("missatge")` troba l'element de l'HTML que té aquest `id`.
- `element.textContent = "text"` canvia el text d'un element.
- `boto.addEventListener("click", alPremerBoto);` diu «quan facin clic, executa aquesta funció». Va **sense parèntesis**: passam la funció, no l'executam.
- Els `<script>` van al final del `<body>`, amb `principal.js` l'últim.

### B11. Log i proves *(log.js, eines-proves.js, verificadors)*

- **Interruptor:** una constant (`const ACTIVAR_LOG = true;`) i un `if` que la consulta dins de `log`.
- Què registrar: l'entrada, les parts, el resultat i els errors capturats.
- **Prova** = comparar el resultat **obtingut** amb l'**esperat** amb `===`.
- Tres tipus de casos: **normals**, **límit** (zero, negatius, decimals, espais) i **invàlids** (han de llançar un error).
- **Prova d'error:** es crida la funció dins d'un `try`. Si no salta cap error, la prova falla; si salta, es comprova `error.name`.
- Comptadors amb `let`: `provesFetes = provesFetes + 1;`.
- Cada prova és **una crida**: no calen llistes ni bucles.
- El verificador prova el **requeriment**, no el codi (prova de caixa negra).

### Quins blocs necessita cada unitat

| Unitat | Blocs |
| --- | --- |
| U1 `entrada.js` | B2, B3, B5, B6, B8, B9 |
| U2 `aritmetica.js` | B4, B5, B6, B9 |
| U3 `calculadora.js` | B5, B6, B7, B9 |
| U4 `pagina.js` | B6, B7, B9, B10 |
| `log.js` i `eines-proves.js` | B2, B4, B5, B6, B11 |
| Verificadors | B3, B4, B6, B9, B11 |

---

## 6. Codi de referència (per l'alumnat)

És el resultat final de la pràctica. **Es dona a l'alumnat**: serveix per orientar i corregir. Només es dona, a la sessió 1, la base dels requeriments.

### Requeriments de les unitats (base per a l'alumnat)

| Unitat | Signatura | Retorna | Errors que llança |
| --- | --- | --- | --- |
| **U1** | `dividirEntrada(entrada)`, amb `entrada` de tipus text o `null` | Un objecte `{ nombre1, operador, nombre2 }` (dos nombres i un text) | `Error` si `entrada` és `null`; `SyntaxError` si el text no té la forma `nombre operador nombre` |
| **U2** | `operar(nombre1, operador, nombre2)` | El resultat (un nombre) | `RangeError` si es divideix o es calcula el mòdul entre 0; `Error` si l'operador no és `+ - * / %` |
| **U3** | `calcular(entrada)` i `alPremerBoto()` | `calcular` retorna el resultat (un nombre). `alPremerBoto` no retorna res: escriu a la pàgina | `calcular` deixa passar els errors de U1 i U2. `alPremerBoto` els captura tots |
| **U4** | `log(text)` i `executarProves(nomUnitat, funcio, proves)` | Res: escriuen a la consola | Cap: `executarProves` captura els errors de la unitat que prova |

### Codi de cada fitxer

**config.js**

```js
// config.js · Interruptors del programa
const ACTIVAR_LOG = true;      // true: missatges de log a la consola
const ACTIVAR_PROVES = true;   // true: executa els plans de proves en carregar la pàgina
```

**log.js** (U4)

```js
// log.js · Unitat U4
// Activació de log: log(text) escriu "[LOG] text" a la consola només si ACTIVAR_LOG és true.

function log(text) {
  if (ACTIVAR_LOG) {
    console.log("[LOG] " + text);
  }
}
```

**dividirEntrada.js** (U1)

```js
// dividirEntrada.js · Unitat U1
// requeriment: rep un text i retorna { nombre1, operador, nombre2 }.
// Errors: Error si entrada és null; SyntaxError si no és "nombre operador nombre".

const patro = /^\s*(-?\d+(?:\.\d+)?)\s*([+\-*/%])\s*(-?\d+(?:\.\d+)?)\s*$/;

function dividirEntrada(entrada) {
  log("Entrada rebuda: " + entrada);

  if (entrada === null) {
    throw new Error("Has cancel·lat l'operació");
  }

  const parts = entrada.match(patro);
  if (parts === null) {
    throw new SyntaxError("L'expressió no és vàlida. Usa: nombre operador nombre");
  }

  const dades = {
    nombre1: parseFloat(parts[1]),
    operador: parts[2],
    nombre2: parseFloat(parts[3])
  };

  log("Dividit en: " + dades.nombre1 + " | " + dades.operador + " | " + dades.nombre2);
  return dades;
}
```

**operar.js** (U2)

```js
// operar.js · Unitat U2
// requeriment: operar(nombre1, operador, nombre2) retorna el resultat.
// Errors: RangeError si es divideix o es calcula el mòdul entre 0;
//         Error si l'operador no és + - * / %

function operar(nombre1, operador, nombre2) {
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
  } else {
    throw new Error("Operador desconegut: " + operador);
  }

  log("Resultat de l'operació: " + resultat);
  return resultat;
}
```

**calculadora.js** (U3)

```js
// calculadora.js · Unitat U3
// requeriment: calcular(entrada) retorna el resultat (un nombre);
//            alPremerBoto() demana l'operació i escriu el resultat o l'error a la pàgina.

const missatge = document.getElementById("missatge");
const boto = document.getElementById("boto");

// No toca la pàgina: així es pot provar sola.
function calcular(entrada) {
  const dades = dividirEntrada(entrada);
  return operar(dades.nombre1, dades.operador, dades.nombre2);
}

// L'únic try / catch del programa (a part de l'executor de proves).
function alPremerBoto() {
  try {
    const entrada = prompt("Escriu una operació, per exemple 3.5 * 2");
    const resultat = calcular(entrada);
    const text = entrada.trim() + " = " + resultat;

    log("Mostrant a la pàgina: " + text);
    missatge.textContent = text;
  } catch (error) {
    log("Error capturat (" + error.name + "): " + error.message);
    missatge.textContent = "Error: " + error.message;
  }
}

boto.addEventListener("click", alPremerBoto);
```

**executor.js** (U4)

```js
// executor.js · Unitat U4
// requeriment: executarProves(nomUnitat, funcio, proves) crida funcio(prova) per a cada
// prova de la llista i escriu OK o ERROR a la consola, amb el recompte final.

function executarProves(nomUnitat, funcio, proves) {
  console.log("--- Proves de " + nomUnitat + " ---");
  let superades = 0;

  for (const prova of proves) {
    let correcta = false;
    let obtingut;

    try {
      obtingut = funcio(prova);
      correcta = (prova.error === undefined &&
                  JSON.stringify(obtingut) === JSON.stringify(prova.esperat));
    } catch (error) {
      obtingut = error.name;
      correcta = (prova.error === error.name);
    }

    if (correcta) {
      superades = superades + 1;
      console.log("OK     " + prova.id + " " + prova.descripcio);
    } else {
      console.log("ERROR  " + prova.id + " " + prova.descripcio +
                  " -> obtingut: " + JSON.stringify(obtingut));
    }
  }

  console.log(superades + " de " + proves.length + " proves superades");
}
```

**proves-dividirEntrada.js** (pla del verificador de U1)

```js
// proves-dividirEntrada.js · Pla de proves de U1

const provesDividirEntrada = [
  { id: "D1", descripcio: "suma senzilla", entrada: "7 + 3",
    esperat: { nombre1: 7, operador: "+", nombre2: 3 } },
  { id: "D2", descripcio: "decimals i sense espais", entrada: "3.5*2",
    esperat: { nombre1: 3.5, operador: "*", nombre2: 2 } },
  { id: "D3", descripcio: "espais sobrants", entrada: "  9   /  2 ",
    esperat: { nombre1: 9, operador: "/", nombre2: 2 } },
  { id: "D4", descripcio: "primer nombre negatiu", entrada: "-7 % 3",
    esperat: { nombre1: -7, operador: "%", nombre2: 3 } },
  { id: "D5", descripcio: "segon nombre negatiu", entrada: "5 - -3",
    esperat: { nombre1: 5, operador: "-", nombre2: -3 } },
  { id: "D6", descripcio: "dues operacions", entrada: "1 + 2 + 3", error: "SyntaxError" },
  { id: "D7", descripcio: "text sense sentit", entrada: "hola", error: "SyntaxError" },
  { id: "D8", descripcio: "decimal sense zero inicial", entrada: ".5 + 1", error: "SyntaxError" },
  { id: "D9", descripcio: "text buit", entrada: "", error: "SyntaxError" },
  { id: "D10", descripcio: "cancel·lar el prompt", entrada: null, error: "Error" }
];

function provarDividirEntrada(prova) {
  return dividirEntrada(prova.entrada);
}
```

**proves-operar.js** (pla del verificador de U2)

```js
// proves-operar.js · Pla de proves de U2

const provesOperar = [
  { id: "O1", descripcio: "suma", nombre1: 7, operador: "+", nombre2: 3, esperat: 10 },
  { id: "O2", descripcio: "resta", nombre1: 10, operador: "-", nombre2: 4, esperat: 6 },
  { id: "O3", descripcio: "multiplicació amb decimal", nombre1: 3.5, operador: "*", nombre2: 2, esperat: 7 },
  { id: "O4", descripcio: "divisió amb decimals", nombre1: 9, operador: "/", nombre2: 2, esperat: 4.5 },
  { id: "O5", descripcio: "mòdul", nombre1: 10, operador: "%", nombre2: 3, esperat: 1 },
  { id: "O6", descripcio: "mòdul amb negatiu", nombre1: -7, operador: "%", nombre2: 3, esperat: -1 },
  { id: "O7", descripcio: "multiplicar per un negatiu", nombre1: 4, operador: "*", nombre2: -3, esperat: -12 },
  { id: "O8", descripcio: "dividir entre zero", nombre1: 8, operador: "/", nombre2: 0, error: "RangeError" },
  { id: "O9", descripcio: "mòdul entre zero", nombre1: 8, operador: "%", nombre2: 0, error: "RangeError" },
  { id: "O10", descripcio: "operador desconegut", nombre1: 2, operador: "x", nombre2: 3, error: "Error" }
];

function provarOperar(prova) {
  return operar(prova.nombre1, prova.operador, prova.nombre2);
}
```

**proves-calcular.js** (pla del verificador de U3)

```js
// proves-calcular.js · Pla de proves de U3 (la part automàtica: calcular)

const provesCalcular = [
  { id: "C1", descripcio: "suma", entrada: "7 + 3", esperat: 10 },
  { id: "C2", descripcio: "decimals", entrada: "3.5*2", esperat: 7 },
  { id: "C3", descripcio: "primer nombre negatiu", entrada: "-5 + 2", esperat: -3 },
  { id: "C4", descripcio: "resta d'un negatiu", entrada: "5 - -3", esperat: 8 },
  { id: "C5", descripcio: "divisió entre zero", entrada: "8 / 0", error: "RangeError" },
  { id: "C6", descripcio: "expressió no vàlida", entrada: "1 + 2 + 3", error: "SyntaxError" },
  { id: "C7", descripcio: "cancel·lar", entrada: null, error: "Error" }
];

function provarCalcular(prova) {
  return calcular(prova.entrada);
}
```

**principal.js** (tot el grup)

```js
// principal.js · Arrancada (l'últim fitxer que es carrega)

function executarTotesLesProves() {
  executarProves("dividirEntrada", provarDividirEntrada, provesDividirEntrada);
  executarProves("operar", provarOperar, provesOperar);
  executarProves("calcular", provarCalcular, provesCalcular);
}

if (ACTIVAR_PROVES) {
  executarTotesLesProves();
}
```

### Proves manuals (les parts que no es poden automatitzar)

| Unitat | Pla de proves manual del verificador |
| --- | --- |
| `alPremerBoto` | Clic i `7 + 3`: el paràgraf mostra `7 + 3 = 10`. Clic i `hola`: mostra `Error: ...`. Clic i *Cancel·lar*: mostra `Error: Has cancel·lat l'operació`. Després d'un error, un clic nou torna a funcionar. |
| `log` | Amb `ACTIVAR_LOG = true` surten missatges `[LOG]`. Amb `false` no en surt cap. |
| `executarProves` | Prova-la amb una funció falsa que sempre retorna `1` i tres proves que esperen `1`, `1` i `2`: ha de mostrar `2 de 3 proves superades`. |

### Com funcionen els interruptors

| `ACTIVAR_LOG` | `ACTIVAR_PROVES` | Què es veu a la consola |
| --- | --- | --- |
| `true` | `true` | Logs i resultats de les proves barrejats (útil per depurar) |
| `false` | `true` | Només el resultat net de les proves |
| `true` | `false` | Només els logs de les operacions que feu amb el botó |
| `false` | `false` | Res: versió «de producció» |

### Idees clau del disseny

- **Cada unitat té un requeriment i un pla de proves.** El verificador prova el **requeriment**, no el codi.
- **`calcular` no toca la pàgina:** rep un text i retorna un nombre (o llança un error). Per això es pot provar sola.
- **Les funcions llancen els errors** i només `alPremerBoto` els captura per avisar l'usuari (i `executarProves`, que els espera).
- Les proves comproven el **tipus d'error** (`error.name`) i no el missatge, perquè l'alumnat pugui canviar els textos sense trencar res.
- Casos que sovint s'obliden i que un bon verificador troba: l'operador desconegut (`O10`), el mòdul amb negatius (`O6`), el text buit (`D9`) i els espais sobrants (`D3`).

---

## 7. Avaluació

La nota combina el treball **individual** (la unitat pròpia i la verificació de la d'un company) i el del **grup** (la integració).

| Criteri | Pes |
| --- | --- |
| **Unitat pròpia:** compleix el requeriment i passa el pla de proves del verificador | 20 % |
| **Pla de proves com a verificador:** mínim 5 proves (normals, límit i invàlides) i informes d'errors clars | 20 % |
| **Calculadora integrada:** 5 operacions, nombres negatius i decimals, resultat a la pàgina | 20 % |
| **Tractament d'errors:** `throw`, `try / catch`, missatges clars | 10 % |
| **Log i interruptors:** `ACTIVAR_LOG` i `ACTIVAR_PROVES` funcionals | 10 % |
| **Qualitat del codi i dels documents:** noms, comentaris, fitxes de requeriment, diari de grup | 5 % |
| **Defensa oral individual** | 15 % |

### Preguntes per a la defensa (qualsevol alumne, qualsevol línia)

- Quin és el requeriment de la teva unitat? Què retorna i quins errors llança?
- Quines proves ha dissenyat el teu verificador? Quin error ha trobat?
- Per què el verificador dissenya les proves sense mirar el codi?
- Què passa si canvio `ACTIVAR_LOG` a `false`? I `ACTIVAR_PROVES`?
- Per què cal `parseFloat`? Què passaria sense?
- Què retorna `match` si el text no encaixa?
- Quina diferència hi ha entre `return` i `throw`?
- Per què `boto.addEventListener("click", alPremerBoto)` no du parèntesis?

### Llista de comprovació abans de lliurar

- La calculadora resol les 5 operacions des del botó.
- Mostra errors clars (entrada invàlida, divisió entre zero, cancel·lar).
- Cada unitat té fitxa de requeriment i pla de proves amb mínim 5 casos.
- Tots els plans de proves se superen.
- Hi ha informes d'errors dels errors trobats i corregits.
- Els dos interruptors funcionen: s'han provat les quatre combinacions.
- El codi té comentaris i noms descriptius, i el diari de grup està omplert.

---

## 8. Errors típics i ampliacions

| Què passa | Causa probable |
| --- | --- |
| No passa res en fer clic | No s'ha guardat el fitxer o no s'ha actualitzat la pàgina (`F5`) |
| `... is not defined` | Errada d'escriptura en un nom, o falta un `<script>` o l'ordre és incorrecte (`principal.js` ha d'anar l'últim) |
| `... has already been declared` | Dues unitats declaren la mateixa `const` o funció: canvieu un nom |
| `Cannot read properties of null` | L'`id` de l'HTML no coincideix amb el de `getElementById` |
| `Unexpected token` | Falta o sobra un parèntesi, una clau `}` o unes cometes |
| El resultat és `34` en comptes de `7` | S'uneixen textos: falta `parseFloat` |
| Totes les proves fallen | Falta un `return` a la funció adaptadora (`provar...`) o a la unitat |
| Una prova falla i el responsable creu que el codi és correcte | Es revisa el **requeriment**: pla de proves i codi han de seguir el mateix text |

### Ampliacions (per als grups que acabin abans)

1. Afegir la **potència** (`**`): canvia la regex de U1 i afegeix un `else if` a U2. El verificador amplia el seu pla.
2. **Arrodonir** el resultat amb `toFixed(2)`. Provar `0.1 + 0.2`.
3. Mostrar els **errors en vermell** (`missatge.style.color`).
4. **Repetir la pregunta** fins que l'entrada sigui vàlida (investigar `while`).
5. Guardar un **historial** d'operacions en una llista amb `push`.
6. Reescriure `operar` com a **mètode** d'un objecte `Calc` (espai de noms) o com una **classe**. El pla de proves ha de continuar passant.
