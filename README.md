# er-unix
Uso de Expresiones Regulares en Unix.

## Expresiones Regulares
Utilizamos las expresiones regulares para denotar lenguajes regulares. Una expresión es regular cuando:
- \Phi es una expresión regular para el lenguaje regular \Phi.
- \(\epsilon\) es una expresión regular para el lenguaje regular { \(\epsilon\) }
- Si a 

Las expresiones regulares son un medio para describir patrones de texto. Imaginemos que no sólo queremos buscar en un texto todas las líneas que contienen una palabra, como por ejemplo COMPUTACION, sino que sólo nos interesan las líneas que empiezan por la palabra COMPUTACION, pero no las que contengan la palabra en cualquier otra posición. Describir el patrón “COMPUTACION” es trivial, tan sólo hay que escribir “COMPUTACION”.

Las expresiones regulares se evalúan carácter a carácter. Las más básicas son simplemente una lista de letras que forman un texto que debe coincidir exactamente con lo que buscamos. Por ejemplo, con la expresión “HUMAN” sólo coincidirá “HUMAN”. Pero por fortuna las expresiones regulares nos permiten hacer búsquedas y substituciones mucho más complejas.

Las expresiones regulares permiten describir este tipo de patrones de texto y muchos más por lo que nos serán de una gran utilidad. Además, en Unix las expresiones regulares tienen un amplio soporte, tanto en las herramientas de procesamiento de ficheros de texto (grep), o en los editores de texto (vi, emacs) como en los lenguajes de programación (Perl, Python). El único inconveniente de las expresiones regulares es que su sintaxis no es trivial y que además varía ligeramente entre distintas herramientas.

Existen rangos y tipos de caracteres predefinidos que podemos utilizar como:
\hline
| POSIX | ASCII | Significado |
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
| (^) | La expresión encaja o coincide al principio de la línea, por ejemplo ^A |
| (?) | La expresión encaja o coincide al final de la línea, por ejemplo A? |
| (\) | Escapa el carácter siguiente a la contrabarra, haciendo que deje de ser un carácter especial, ejemplo in \* |
| ([])  | La expresión encaja o coincide con alguno de los caracteres incluidos entre los corchetes, también se puden especificar rangos, por ejemplo [aeiou] o [0-9].  |
| [^ ]  | La expresión encaja o coincide con cualquier carácter excepto los que se encuentran entre corchetes, ejemplo, todos los carácteres excepto del 0 al 9: [^0-9] |
| (.) | La expresión encaja respecto a un único carácter, de cualquier valor, excepto al final de la línea. |
| (*) | La expresión coincide con 0 o más carácteres de la expresión que le precede.  |
| \{x,y\} | La expresión encaja o coincide desde X hasta Y respecto a lo que la ocurrencia que le precede.  |
| \{x\} | La expresión encaja exactamente X ocurrencias de lo que le precede. |
| \{x,\}  | La expresión encaja exactamente X o más ocurrencias de lo que le precede. |



### Comodines
El uso de un comodín \* nos permite indicar
