## Лекция 9. БЧХ-коды и РС-коды

## 1. Общая идея

Боуз, Рой-Чоудхури, Хоквингем - БЧХ-коды.

Рид,Соломон -> граница Синглтона:

$$
d \le m + 1 = n - k + 1
$$

Расстояния:

$1$ - кодов нет

$2$ - код с проверкой на четность

$3$ - код Хэмминга

$4$ - расширенный код Хэмминга

## 2. Код Хэмминга через проверочную матрицу

Проверочная матрица:

$$
H =
\begin{pmatrix}
1 & 0 & 1 & 0 & 1 & 0 & 1 \\
0 & 1 & 1 & 0 & 0 & 1 & 1 \\
0 & 0 & 0 & 1 & 1 & 1 & 1
\end{pmatrix}
$$

Столбцы - ненулевые элементы поля $GF(2^3)$.

Поле:

$$
GF(2) \to GF(2^3)
$$

Многочлен:

$$
p(x)=x^3+x+1
$$

$\alpha$ - примитивный элемент.

$$
\begin{aligned}
\alpha^0 &= 1 \\
\alpha^1 &= x \\
\alpha^2 &= x^2 \\
\alpha^3 &= 1+x \\
\alpha^4 &= x+x^2 \\
\alpha^5 &= 1+x+x^2 \\
\alpha^6 &= 1+x^2
\end{aligned}
$$

Набор совпадает с ненулевыми элементами поля, порядок может быть другим.

$$
H =
\begin{pmatrix}
1 & \alpha^1 & \alpha^2 & \alpha^3 & \alpha^4 & \alpha^5 & \alpha^6
\end{pmatrix}
$$

В двоичном виде:

$$
H =
\begin{pmatrix}
1 & 0 & 0 & 1 & 0 & 1 & 1 \\
0 & 1 & 0 & 1 & 1 & 1 & 0 \\
0 & 0 & 1 & 0 & 1 & 1 & 1
\end{pmatrix}
$$

Каждый столбец - один ненулевой элемент поля $GF(2^3)$.

## 3. Переход к коду длины 15

Код с параметрами $(15,11)$.

Поле:

$$
GF(2) \to GF(2^4)
$$

Многочлен:

$$
p(x)=1+x+x^4
$$

Проверочная матрица:

$$
H =
\begin{pmatrix}
1 & \alpha & \alpha^2 & \ldots & \alpha^{14}
\end{pmatrix}
$$

Передано $c(x)$, ошибка $e(x)$, принято:

$$
b(x)=c(x)+e(x)
$$

Синдром:

$$
\begin{aligned}
s
&= \sum_{i=0}^{n-1} b_i\alpha^i \\
&= \sum_{i=0}^{n-1}(c_i+e_i)\alpha^i \\
&= \sum_{i=0}^{n-1}e_i\alpha^i \\
&= e(\alpha)
\end{aligned}
$$

Если ошибка в позиции $i$, то

$$
e(x)=x^i
$$

$$
s=\alpha^i
$$

Если ошибок две:

$$
e(x)=x^i+x^j,\quad i\ne j
$$

Нужна еще одна проверочная строка.

## 4. Исправление двух ошибок

Проверочная матрица:

$$
H =
\begin{pmatrix}
1 & \alpha & \alpha^2 & \ldots & \alpha^{14} \\
\beta_1 & \beta_2 & \beta_3 & \ldots & \beta_{15}
\end{pmatrix}
$$

$$
\beta_i \in GF(2^m)
$$

Если ошибки в позициях $i$ и $j$:

$$
S_1=\alpha^i+\alpha^j
$$

$$
S_2=f(\alpha^i)+f(\alpha^j)
$$

$f(\alpha)=c\alpha$ и $f(\alpha)=\alpha^2$ не помогают.

Берем:

$$
f(\alpha)=\alpha^3
$$

Тогда:

$$
H =
\begin{pmatrix}
1 & \alpha^1 & \alpha^2 & \alpha^3 & \alpha^4 & \alpha^5 & \alpha^6 & \alpha^7 & \alpha^8 & \alpha^9 & \alpha^{10} & \alpha^{11} & \alpha^{12} & \alpha^{13} & \alpha^{14} \\
1 & \alpha^3 & \alpha^6 & \alpha^9 & \alpha^{12} & 1 & \alpha^3 & \alpha^6 & \alpha^9 & \alpha^{12} & 1 & \alpha^3 & \alpha^6 & \alpha^9 & \alpha^{12}
\end{pmatrix}
$$

## 5. Поиск позиций ошибок

Ошибки стоят в $i$ и $j$.

$$
x=\alpha^i,\quad y=\alpha^j
$$

Система:

$$
\begin{aligned}
x+y &= S_1 \\
x^3+y^3 &= S_2
\end{aligned}
$$

При одной или двух ошибках:

$$
S_1\ne0
$$

$$
\frac{x^3+y^3}{x+y}=\frac{S_2}{S_1}
$$

$$
x^3+y^3=(x+y)(x^2+y^2+xy)
$$

$$
x^2+y^2+xy=\frac{S_2}{S_1}
$$

В поле характеристики $2$:

$$
(a+b)^2=a^2+2ab+b^2=a^2+b^2
$$

$$
\begin{aligned}
x+y &= S_1 \\
(x+y)^2 &= S_1^2 \\
x^2+y^2 &= S_1^2
\end{aligned}
$$

$$
S_1^2+xy=\frac{S_2}{S_1}
$$

$$
xy=\frac{S_2}{S_1}-S_1^2
$$

По теореме Виета:

$$
z^2+\sigma_1z+\sigma_2=0
$$

$$
\sigma_1=S_1
$$

$$
\sigma_2=\frac{S_2}{S_1}-S_1^2
$$

Корни - $x$ и $y$, то есть $\alpha^i$ и $\alpha^j$.

## 6. Поле $GF(2^4)$

Поле:

$$
GF(2) \to GF(2^4)
$$

Многочлен:

$$
p(x)=1+x+x^4
$$

Степени $\alpha$:

$$
\begin{aligned}
\alpha^0 &= 1 = 0001 \\
\alpha^1 &= x = 0010 \\
\alpha^2 &= x^2 = 0100 \\
\alpha^3 &= x^3 = 1000 \\
\alpha^4 &= 1+x = 0011 \\
\alpha^5 &= x+x^2 = 0110 \\
\alpha^6 &= x^2+x^3 = 1100 \\
\alpha^7 &= 1+x+x^3 = 1011 \\
\alpha^8 &= 1+x^2 = 0101 \\
\alpha^9 &= x+x^3 = 1010 \\
\alpha^{10} &= 1+x+x^2 = 0111 \\
\alpha^{11} &= x+x^2+x^3 = 1110 \\
\alpha^{12} &= 1+x+x^2+x^3 = 1111 \\
\alpha^{13} &= 1+x^2+x^3 = 1101 \\
\alpha^{14} &= 1+x^3 = 1001
\end{aligned}
$$

## 7. Пример исправления двух ошибок

Ошибки в позициях $2$ и $9$.

Синдромы:

$$
S_1=\alpha^2+\alpha^9=\alpha^{11}
$$

$$
S_2=\alpha^6+\alpha^{12}=\alpha^4
$$

$$
xy=\frac{S_2}{S_1}-S_1^2
$$

Подставим:

$$
xy=\frac{\alpha^4}{\alpha^{11}}+(\alpha^{11})^2
$$

Так как период поля $15$:

$$
\begin{aligned}
\frac{\alpha^4}{\alpha^{11}}+(\alpha^{11})^2
&= \frac{1}{\alpha^7}+\alpha^7 \\
&= \frac{1+\alpha^{14}}{\alpha^7} \\
&= \frac{\alpha^3}{\alpha^7} \\
&= \alpha^{-4}
\end{aligned}
$$

$$
\sigma_2=\alpha^{-4}=\alpha^{11}
$$

$$
\sigma_1=\alpha^{11}
$$

Уравнение локатора ошибок:

$$
z^2+\alpha^{11}z+\alpha^{11}=0
$$

Для $z=\alpha^2$:

$$
\begin{aligned}
(\alpha^2)^2+\alpha^{11}\alpha^2+\alpha^{11}
&= \alpha^4+\alpha^{13}+\alpha^{11} \\
&= 1+x+1+x^2+x^3+x+x^2+x^3 \\
&= 0
\end{aligned}
$$

Для $z=\alpha^9$:

$$
\begin{aligned}
(\alpha^9)^2+\alpha^{11}\alpha^9+\alpha^{11}
&= \alpha^3+\alpha^5+\alpha^{11} \\
&= x^3+x+x^2+x+x^2+x^3 \\
&= 0
\end{aligned}
$$

$\alpha^2$ и $\alpha^9$ - корни.

Ошибки в позициях $2$ и $9$.
