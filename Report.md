# Задание лабораторной работы
На основе изученного материала лабораторной работы, лекций (2 и 3), дополнительных источников напишите скрипт, который на вход принимает IPv4-адрес в десятичном формате, а на выходе обеспечивает данный IP-адрес в двоичном формате.
## Полный код решения
![image](https://github.com/user-attachments/assets/16801f1d-0e5d-4749-b86a-d796bfd8d64f)
## Разложим наше задание на подзадачи и на примере их выполнения разберем решение:
1) Создаем массив из входной строки с разделением по символу "." 

   ![image](https://github.com/user-attachments/assets/62d4cf6f-9ba8-404a-bd00-c196de9d6e74)

   Для этого:
   
   a) Указываем символ-разделитель в специальной переменной IFS 

   b) Создаем переменную count и присваиваем ей значение 0, она понадобится нам позже для образения к элементам массива.
   
   с) Выводим на экран просьбу к пользователю ввести IPv4: echo "enter your IPv4"

   d) С помощью функции read считываем введенную пользователем строку в переменную IPv4

   e) Также с помощью фцнкции read -a создаем массив array из строки IPv4 по указанному ранее разделителю IFS

---

2) Далеее решение осуществляется с помощью вложенных циклов, поэтому для удобства рассмотрим проблемы перевода элементов массива в 2-ю СС, дозаполнением нулями до 8-bit-го вида и обновления элементов массива, вместе:

   ![image](https://github.com/user-attachments/assets/5c0b0d34-73bb-442e-bb58-b74b624fc6ac)

   Для этого:

   a) Создаем цикл for i in "${array[@]}", который в каждой итерации цикла будет присваивать переменной i новый элемент массива, пока элемеенты в массиве не закончатся, так мы перебираем все числа, составляющие IPv4.

   b) Далее создаем цикл while ((i > 0)), в котором приводим значение массива, записанное в i к двоичному формату. Осуществяляется это с помощью взятия остатка от деления i на 2 $((i % 2)), добавлением этого значения в строку bin = "$d$bin" (именной в таком порядке) и перезаписыванием i после целочисленного деления на 2 i = $((i // 2))

   c) После окончания работы цикла while мы получаем двоичное представление числа i, записанное в переменную bin. Обрааясь по индексу $count перезаписываем i значением bin array[$count] = $(printf "%08d" "$bin").

   d) Однако, мы не можем использовать bin напрямую, так как bin может содержать двоичное число, которое будет состоять из меньше чем 8 символов, в таком случае мы должны форматировать его и дописать в это чсло нужное количество ведущих нулей. Для этого мы используем команду $(printf "%08d" "$bin"), где printf - команда, позволяющая форматировать вывод, "%08d" - форматная строка, задающая как именно должен выглядет выход команды.

   e) Перезаписываем count = $((count + 1)) с увеличенным на 1 значения для работы со следующим i в новой итерации 

---

3) Вывод результата работы:

   a) После выхода из всех циклов массив будет перезаписан отформатированными, двоичными значениями Ipv4. Нам остается лишь вывести весь массив, соединяю его элементы ".": echo "${array[*]}"

### Примеры работы программы: 

![image](https://github.com/user-attachments/assets/4a0f5d1a-a631-4ca9-9434-98bcef2c999b)

![image](https://github.com/user-attachments/assets/3d55c8c7-0e80-4f02-9f89-80bf0e71b532)

![image](https://github.com/user-attachments/assets/bf0291b4-9cd9-457c-8e25-6bd625d913e6)

![image](https://github.com/user-attachments/assets/ef325c8d-dde4-4d07-95f2-507ca583329b)





   
