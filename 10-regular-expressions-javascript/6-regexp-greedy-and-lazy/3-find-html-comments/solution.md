Нужно найти начало комментария `match:<!--`, затем всё до конца `match:-->`.

С первого взгляда кажется, что это сделает регулярное выражение `pattern:<!--.*?-->` -- квантификатор сделан ленивым, чтобы остановился, достигнув `match:-->`.

Однако, точка в JavaScript -- любой символ, *кроме* конца строки. Поэтому такой регэксп не найдёт многострочный комментарий.

Всё получится, если вместо точки использовать полностю "всеядный" `pattern:[\s\S]`.

Итого:

```js run
var re = /<!--[\s\S]*?-->/g;

var str = '.. <!-- Мой -- комментарий \n тест --> ..  <!----> .. ';

alert( str.match(re) ); // '<!-- Мой -- комментарий \n тест -->', '<!---->'
```
