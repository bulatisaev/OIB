﻿Лабораторная работа №8![ref1]![ref2]

Элементы криптографии. 

Шифрование (кодирование) различных исходных текстов одним ключом![ref3]![ref3]

**Исаев Булат Абубакарович Студ. Билет: 1132227131 Группа: НПИбд-01-22** 

Шифр гаммирования - наложение криптографической гаммы на данные для ![ref1]![ref2]получения зашифрованных данных. Он основан на генерации гаммы шифра с помощью псевдослучайных чисел и ее наложении на открытые данные    обратимым образом. Дешифрование сводится к повторной генерации       гаммы шифра и ее наложению на зашифрованные данные.               ![ref3]![ref3]Криптостойкость определяется размером ключа. Метод становится         неприменимым, если известен фрагмент исходного текста и              соответствующая шифрограмма. Метод с обратной связью включает        генерацию гаммы с использованием контрольной суммы участка данных

Идея взлома заключается в получении открытого текста путем сравнения       ![ref1]![](images/4.png)шифротекстов двух телеграмм, зашифрованных одним ключом. При помощи операции XOR можно найти открытый текст, зная значение шифротекстов.    Предположим, что одна из телеграмм имеет фиксированный формат, известный  ![ref3]![ref3]

злоумышленнику. Тогда он может определить символы открытого сообщения,  находящиеся на позициях известного шаблона сообщения. Действуя поэтапно, злоумышленник может уменьшить пространство поиска открытого текста значительно

**Рис. 1 –** Код (1 часть)![ref1]![ref2]![](images/5.jpeg)![ref3]![ref3]

**Рис. 2 –** Код (2 часть)![ref1]![ref2]![](images/6.jpeg)![ref3]![ref3]

**Рис. 3 –** Код (3 часть)![](images/7.png)![ref2]![](images/8.jpeg)![ref3]![ref3]

Вывод![](images/9.jpeg)![](images/10.png)

В ходе выполнения лабораторной работы было разработано приложение,  ![ref4]![ref4]позволяющее шифровать тексты в режиме однократного гаммирования. 

[ref1]: images/1.png
[ref2]: images/2.png
[ref3]: images/3.png
[ref4]: images/11.png