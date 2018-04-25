# er-unix
Uso de Expresiones Regulares en Unix.

## Expresiones Regulares
Utilizamos las expresiones regulares para denotar lenguajes regulares. Una expresión es regular cuando:
- <em> &Phi; </em> es una expresión regular para el lenguaje regular <em> &Phi; </em>.
- <em> &epsilon; </em> es una expresión regular para el lenguaje regular { <em> &epsilon; </em> }.
- Si a <em> &straightepsilon; </em> <em> &Sigma; </em> (donde Sigma es el alfabeto), a es una expresión regular con lenguaje {a}.
- Si a y b son expresiones regulares, entonces a + b también lo será, cuyo lenguaje ha de ser {a,b}.
- Si a y b son expresiones regulares, entonces ab (es decir la concatenación) también será regular.
- Si a es una expresión regular, luego a\* (0 o más veces a) también lo será.

Es así que tenemos:

|                          | Expresion Regular| Lenguaje Regular  |
| ------------------------ |:----------------:| -----------------:|
| conjunto de vocales      | aueieiaoieoieieiu|    {a,e,i,o,u}    |
| b, de ahí 0 o más c      |      (b.c*)      |{b,bc,bcc,bccc... }|


### Gramática Regular
Una gramática es regular cuando tiene un conjunto de reglas de la forma A -> a, o A -> aB o A -> <em> &epsilon; </em>, donde épsilon es el caracter especial llamado NULL.

### Lenguaje Regular
Un lenguaje será regular, si puede ser expresado en términos de su expresión regular.

### Expresiones Regulares en UNIX

Las expresiones regulares son un medio para describir patrones de texto. Imaginemos que no sólo queremos buscar en un texto todas las líneas que contienen una palabra, como por ejemplo COMPUTACION, sino que sólo nos interesan las líneas que empiezan por la palabra COMPUTACION, pero no las que contengan la palabra en cualquier otra posición. Describir el patrón “COMPUTACION” es trivial, tan sólo hay que escribir “COMPUTACION”.

Las expresiones regulares se evalúan carácter a carácter. Las más básicas son simplemente una lista de letras que forman un texto que debe coincidir exactamente con lo que buscamos. Por ejemplo, con la expresión “HUMAN” sólo coincidirá “HUMAN”. Pero por fortuna las expresiones regulares nos permiten hacer búsquedas y substituciones mucho más complejas.

Las expresiones regulares permiten describir este tipo de patrones de texto y muchos más por lo que nos serán de una gran utilidad. Además, en Unix las expresiones regulares tienen un amplio soporte, tanto en las herramientas de procesamiento de ficheros de texto (grep), como en los editores de texto (vi, emacs) como en los lenguajes de programación (Perl, Python). El único inconveniente de las expresiones regulares es que su sintaxis no es trivial y que además varía ligeramente entre distintas herramientas.

Existen rangos y tipos de caracteres predefinidos que podemos utilizar como:


| POSIX | ASCII | Significado |
| ------------- |:-------------:| -----:|
| [:alnum:] | [A-Za-z0-9] | Caracteres alfanuméricos (letras y números) |
| [:word:]  | [A-Za-z0-9_]  | Caracteres alfanuméricos y “_”  |
| [:alpha:] | [A-Za-z]  | Caracteres alfabéticos  |
| [:blank:] | [ \t] | Espacio y tabulador |
| [:space:] | [ \t\r\n\v\f] | Espacios  |
| [:digit:] | [0-9] | Dígitos |
| [:lower:] | [a-z] | Letras minúsculas |
| [:upper:] | [A-Z] | Letras mayúsculas |
| [:punct:] | [][!”#$%&’()*+,./:;<=>?@\^_`{\|}~-] | Caracteres de puntuación  |

####Cuantificadores:
Además de indicar qué caracteres queremos permitir podemos seleccionar cuantas veces deben aparecer. Si no añadimos nada que indique lo contrario se asume que el carácter debe aparecer una vez, pero podríamos pedir que el carácter aparezca un número distinto de veces:

  *	”?”, el carácter aparece ninguna o una vez.
    Por ejemplo: “usher1?” coincidiría con “usher” o “usher1”.
  *	”*”, cero, una o varias veces.
  *	”+”, al menos una vez.
  *	“{4}”, cuatro veces.
  *	“{4,10}”, entre 4 y 10 veces

####Puntos de anclaje:
Además de poder indicar qué y cuántas veces queremos que algo aparezca podemos indicar dónde deseamos que lo haga. Los puntos de anclaje más utilizados son:

  *	”^”, inicio de línea
  *	”$”, fin de línea
  *	”<”, principio de palabra
  *	”>”, fin de palabra
  *	“\b”, límite de palabra

####Nota:
Algunos caracteres tienen significados especiales, como ., $, (, ), [, ], \ o ^ y si se quieren utilizar hay que escaparlos precediéndolos con \.

Ejemplos:
```bash
$ # Listar todas las líneas que comienzan por "From:" de nuestros emails:
$ grep '^From: ' /usr/mail/$USER
$ # Buscar líneas con al menos una letra desde la “a” hasta la “z” (incluidas mayúsculas) de un fichero concreto.
$ grep '[a-zA-Z]' search-file.txt
$ # Lista cualquier carácter que no sea ni letra ni número de un archivo.
$ grep '[^a-zA-Z0-9]' search-file.txt
$ # Buscar teléfonos del tipo 999-9999 de un fichero concreto.
$ grep '[0-9]\{3\}-[0-9]\{4\}' search-file.txt
$ # Buscar líneas de un fichero con solamente 1 carácter:
$ grep '^.$' search-file.txt
$ # Buscar líneas que comienzan con el carácter "."
$ grep '^\.' search-file.txt
$ # Buscar líneas que comienzan por un "." y dos letras en minúscula:
$ grep '^\.[a-z][a-z]' search-file.txt
```

### Aplicaciones en UNIX
#### Grep
Grep o Global Regular Expression print, es una utilidad de la línea de comando que nos permite realizar búsquedas en _data sets_ de archivos de texto; línea a línea, y compararlas con una expresión regular. Es una de las más útiles y versátiles que nos trae la línea de comandos de Linux, y es extremadamente poderoso si es utilizado de manera apropiada.

```bash
cd /usr/share/common-licenses
grep "GNU" GPL-3
```
El primer argumento, "GNU", es el patrón que deseamos buscar, mientras que el segundo argumento, "GPL-3", es el fichero de entrada que deseamos buscar. Esto tendrá como resultado, todas y cada una de las líneas que contienen dicho patrón en el texto.

##### Opciones
Asimismo, podemos hacer uso de flags o banderas que nos permiten acceder a una amplia gama de opciones. Podemos utilizar **-v**  o **--invert-match** para hacer una búsqueda invertida que deje afuera a la expresión especificada. También está la bandera **-i** o **--ignore-case** que nos permite ignorar si se trata de caracteres en mayúscula o minúscula, durante la búsqueda y devolver el resultado independientemente de ello.

#### Sed
Editor de flujo; permite realizar transformaciones básicas de un flujo de entrada (un fichero o una entrada desde una tubería) 
Formato (para substituciones):
```bash
sed [opciones] 's/REGEXP/reemplazo/flag' [fichero]
```
Algunos comandos:
*	s substitución
*	d borrado
*	i\, a\, añade antes/después de la línea afectada
*	c\ reemplaza la línea afectada
Algunas opciones:
*	-e comando: añade comando
*	-i edita el fichero in-place
*	-n suprime la salida
Algunos flags:
*	g: aplica los cambios globalmente (por defecto, sólo se cambia la primera aparición en cada línea)
*	p imprime las líneas afectadas, incluso con la opción -n.
*	NUMERO: reemplaza la aparición número NUMERO.
*	w fichero: escribe las líneas con sustituciones al fichero indicado.

Ejemplos:
*	Cambia, en el fichero amigos, todas las apariciones de pepe y paco por Pepe y Paco, respectivamente:
```bash
$ sed -e 's/pepe/Pepe/g' -e 's/paco/Paco/g' amigos
```
también...
```bash
sed 's/pepe/Pepe/g ; s/paco/Paco/g' amigos
```
*	Cambia pepe por Pepe, pero sólo en las líneas que tengan Potamo
```bash
$ sed '/Potamo/s/pepe/Pepe/g' amigos
```
*	Muestra sólo las líneas que contengan jaime
```bash
$ sed -n '/jaime/p' amigos
```
*	Borra las líneas que contengan jaime
```bash
$ sed '/jaime/d' amigos
```
*	Cambia las líneas que contengan jaime por otra cosa
```bash
$ sed '/jaime/c\BORRADO' amigos
```
*	Inserta una línea, con la palabra 'APARICION', antes de las líneas que contengan jaime
```bash
$ sed '/jaime/i\APARICION' amigos
```
*	Reemplaza, en cada línea de fichero, la quinta ocurrencia de stop por STOP
```bash
$ sed 's/stop/STOP/5' fichero
```
*	Igual que antes, pero guarda cada línea reemplazada en el fichero f2
```bash
$ sed 's/stop/STOP/5w f2' fichero
```
#### Indicación de líneas:
Podemos especificar las líneas del fichero en las que queremos que se realicen las operaciones:
```bash
sed '3s/stop/STOP/g' #reemplaza sólo en la línea 3
sed '3,10s/stop/STOP/g' #reemplaza de la línea 3 a la 10
sed '3,$s/stop/STOP/g' #reemplaza de la línea 3 al final 
sed '!3s/stop/STOP/g' #reemplaza en todas las líneas menos la 3
```

### NOTA:
#### Operador &:
Se sustituye el patrón reconocido.
Ejemplo: Reemplazar stop por <stop>
 ```bash
 $ sed '3s/stop/<&>/g' fichero
 ```
#### Operador . :
Indica la existencia de un caracter en su ubicación.
