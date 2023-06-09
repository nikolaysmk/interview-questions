# Проверка строки на палиндром

Для начала, что такое палиндром? Это слово или фраза, которые одинаково читаются в обоих направлениях. Например, "шалаш", "топот", "а роза упала на лапу Азора".

Задача этого кода - проверить, является ли строка палиндромом. Это может быть полезно, например, для проверки правильности написания отзывов или комментариев, чтобы убедиться, что они не содержат никакого нежелательного контента.

Для этого используется два подхода:

1.  Метод фильтрации алфавитно-цифровых символов из строки, далее создание копии строки в обратном порядке и сравнение двух строк.
2.  Метод двух указателей.

Первый метод более затратный по памяти, но при этом более лаконичный и понятный. Он работает следующим образом:

1.  Если строка пустая, то она является палиндромом, возвращаем true.
2.  Создаем новую строку, в которой будут только алфавитно-цифровые символы (убираем все остальные). Это делается с помощью функции filterAlphaNumeric, которая использует методы toLowerCase() и replace() для фильтрации строк.
3.  Создаем еще одну строку, которая является копией предыдущей, но в обратном порядке. Для этого используется функция reverse, которая разбивает строку на массив символов, меняет порядок элементов в массиве и объединяет их обратно в строку.
4.  Сравниваем две строки. Если они равны, то наша исходная строка является палиндромом, возвращаем true, иначе возвращаем false.

```javascript
/**
 * Array - Filter && Clone && Reverse
 * Time O(N) | Space O(N)
 * https://leetcode.com/problems/valid-palindrome/
 * @param {string} s
 * @return {boolean}
 */
var isPalindrome = function(s) {
    if (!s.length) return true;
    
    const alphaNumeric = filterAlphaNumeric(s);/* Time O(N) | Space O(N) */
    const reversed = reverse(alphaNumeric);    /* Time O(N) | Space O(N) */
    
    return alphaNumeric === reversed;
};

const filterAlphaNumeric = (s, nonAlphaNumeric = new RegExp('[^a-z0-9]','gi')) => s
    .toLowerCase()               /* Time O(N) | Space O(N) */
    .replace(nonAlphaNumeric, '')/* Time O(N) | Space O(N) */

const reverse = (s) => s
    .split('')/* Time O(N) | Space O(N) */
    .reverse()/* Time O(N) | Space O(N) */
    .join('');/* Time O(N) | Space O(N) */

```


Второй метод более лаконичный по памяти, но при этом сложнее понять. Он работает следующим образом:

1.  Если строка пустая или состоит из одного символа, то она является палиндромом, возвращаем true.
2.  Создаем два указателя - left и right, которые указывают соответственно на первый и последний символы строки.
3.  Пока left меньше right:
    -   Получаем символы, на которые указывают left и right.
    -   Если символ, на который указывает left - не алфавитно-цифровой, то переходим на следующий символ, увеличивая left на 1.
    -   Если символ, на который указывает right - не алфавитно-цифровой, то переходим на предыдущий символ, уменьшая right на 1.
    -   Если символы, на которые указывают left и right, являются алфавитно-цифровыми, то сравниваем их. Если они не равны, то строка не является палиндромом, возвращаем false.
    -   Если символы равны, то переходим на следующую пару символов, увеличивая left на 1 и уменьшая right на 1.
4.  Если прошли все символы и не было возвращено false, значит строка является палиндромом, возвращаем true.

Таким образом, мы можем проверить, является ли строка палиндромом, используя два разных метода. Выбор метода зависит от наших предпочтений и требований к памяти.

Если вы хотите использовать первый метод, то вам нужно вызвать функцию isPalindrome и передать ей строку для проверки.

Если вы хотите использовать второй метод, то вам также нужно вызвать функцию isPalindrome и передать ей строку для проверки.

Надеюсь, это поможет вам лучше понять, как работает проверка строки на палиндром, и использовать ее в своих проектах!


```javascript
/**
 * 2 Pointer | Midde Convergence
 * Time O(N) | Space O(1)
 * https://leetcode.com/problems/valid-palindrome/
 * @param {string} s
 * @return {boolean}
 */
var isPalindrome = function(s) {
    if (s.length <= 1) return true;
    
    let [left, right] = [0, s.length - 1];
    let leftChar, rightChar;
    while (left < right) {
        leftChar = s[left];
        rightChar = s[right];
        
        // skip char if non-alphanumeric
        if (!/[a-zA-Z0-9]/.test(leftChar)) {
            left++;
        } else if (!/[a-zA-Z0-9]/.test(rightChar)) {
            right--;
        } else {
            // compare letters
            if (leftChar.toLowerCase() != rightChar.toLowerCase()) {
                return false;
            }
            left++;
            right--;
        }
    }
    return true;
};

```