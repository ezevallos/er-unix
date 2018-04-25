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

Además de expresiones complementarias que nos ayudarán mucho en lo que necesitemos:

|     |                                                                                                       |
|-----|:-----------------------------------------------------------------------------------------------------:|
| (^) | La expresión encaja o coincide al principio de la línea, por ejemplo ^A |
| (?) | La expresión encaja o coincide al final de la línea, por ejemplo A? |
| (\) | Escapa el carácter siguiente a la contrabarra, haciendo que deje de ser un carácter especial, ejemplo en \* |
| (\[\])  | La expresión encaja o coincide con alguno de los caracteres incluidos entre los corchetes, también se pueden especificar rangos, por ejemplo \[aeiou\] o \[0-9\].  |
| \[^ \]  | La expresión encaja o coincide con cualquier carácter excepto los que se encuentran entre corchetes, ejemplo, todos los carácteres excepto del 0 al 9: \[^0-9\] |
| (.) | La expresión encaja respecto a un único carácter, de cualquier valor, excepto al final de la línea. |
| (*) | La expresión coincide con 0 o más carácteres de la expresión que le precede.  |
| \{x,y\} | La expresión encaja o coincide desde X hasta Y respecto a lo que la ocurrencia que le precede.  |
| \{x\} | La expresión encaja exactamente X ocurrencias de lo que le precede. |
| \{x,\}  | La expresión encaja exactamente X o más ocurrencias de lo que le precede. |

### Aplicaciones en UNIX
#### Grep
Grep o Global Regular Expression print, es una utilidad de la línea de comando que nos permite realizar búsquedas en _data sets_ de archivos de texto; línea a línea, y compararlas con una expresión regular. Es una de las más útiles y versátiles que nos trae la línea de comandos de Linux, y es extremadamente poderoso si es utilizado de manera apropiada.
´´´bash
cd /usr/share/common-licenses
grep "GNU" GPL-3
´´´bash
