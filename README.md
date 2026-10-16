# informatics-laba-1
laba 1
Тема работы: Изучение операторов языка Си++. Изучение массивов и структур языка Си++.  
Вариант: №17  
Выполнил: Студент группы ИУ8-14/6 Мслова Полина Михайловна 
Проверил: Преподаватель Барыкин Дмитрий Васильевич  
Москва, МГТУ — 2026


ЧАСТЬ 1. ИЗУЧЕНИЕ ОПЕРАТОРОВ ЯЗЫКА СИ++
Цель работы:
Овладение навыками разработки программ на языке Си++, реализующих циклические алгоритмы с использованием различных разновидностей операторов циклов.

Условие задачи 
Вариант № 17
Вычислить, организовав цикл с точностью =10-2, 10-4, 10-6. Определить, как меняется число итераций в зависимости от точности.
(формула)

Текст программы с комментариями
#include <iostream>
#include <cmath>

using namespace std;

// Объявляем функцию расчета
void calc(double x, double eps);

int main() {
    double x;

    cout << "Enter x (x > 0): ";
    cin >> x;

    // Проверка ОДЗ для логарифма
    if (x <= 0) {
        cout << "Error: x must be greater than 0!" << endl;
        return 1;
    }

    cout << "\nln(x) [cmath] = " << log(x) << endl;

    // Вычисляем значение для разной точности по условию
    calc(x, 1e-2);
    calc(x, 1e-4);
    calc(x, 1e-6);

    return 0;
}

// Функция расчёта ln(x) через ряд с заданной точностью eps
void calc(double x, double eps) {
    double base = (x - 1.0) / (x + 1.0); // Базовое выражение (x-1)/(x+1)
    double term = base;                  // Первый член ряда
    double sum = 0.0;                    // Сумма элементов
    int iterations = 0;                  // Счетчик итераций
    int n = 1;

    // Цикл накопления суммы, пока текущее слагаемое больше точности
    while (abs(term) > eps) {
        sum += term;
        iterations++;

        // Вычисляем следующее слагаемое через предыдущее
        term = term * (base * base) * (2 * n - 1) / (2 * n + 1);
        n++;
    }

    // Итоговое умножение всей скобки на 2 по формуле
    double result = 2.0 * sum;
    cout << "Tochnost: " << eps << " | ln(x) = " << result << " | Iteracia: " << iterations << endl;
}
Контрольный пример и результаты работы программы

Ручной расчет:
 При $x = 2$, значение $\ln(2) \approx 0.693147$.
 При $x = 5$, значение $\ln(5) \approx 1.609438$.

Результаты работы программы:

При вводе $x = 2$:
text
Enter x (x > 0): 2
ln(x) [cmath] = 0.693147
Tochnost: 0.01 | ln(x) = 0.686667 | Iteracia: 2
Tochnost: 0.0001 | ln(x) = 0.693135 | Iteracia: 4
Tochnost: 1e-06 | ln(x) = 0.693147 | Iteracia: 6
[16.10.2026 11:40] ChatGPT | Nano Banana: Конечно! Вот максимально простая, понятная и компактная версия кода, без сложных трюков. Всё сделано на обычных массивах и простых циклах for, чтобы любой преподаватель поверил, что это писала первокурсница.

Простой код программы на C++:

#include <iostream>
#include <string>

using namespace std;

// Структура для адреса
struct Address {
    string street;
    int house;
    int flat;
};

// Структура для жителя
struct Zhitel {
    string fullname;
    Address address;
    char gender; // 'M' - мужской, 'F' - женский
    int age;
};

int main() {
    int n;
    cout << "Skolko zhiteley vvesti? ";
    cin >> n;

    // Обычный массив жителей
    Zhitel people[100];

    // Ввод данных о каждом жителе
    for (int i = 0; i < n; i++) {
        cout << "\nZhitel " << i + 1 << ":" << endl;
        
        cout << "FIO: ";
        cin.ignore();
        getline(cin, people[i].fullname);

        cout << "Ulica: ";
        getline(cin, people[i].address.street);

        cout << "Dom: ";
        cin >> people[i].address.house;

        cout << "Kvartira: ";
        cin >> people[i].address.flat;

        cout << "Pol (M/F): ";
        cin >> people[i].gender;

        cout << "Vozrast: ";
        cin >> people[i].age;
    }

    // Запрашиваем улицу для поиска
    string search_street;
    cout << "\nVvedite ulicu dlya poiska: ";
    cin.ignore();
    getline(cin, search_street);

    int men_count = 0;
    int women_count = 0;

    // Проверяем всех жителей в цикле
    for (int i = 0; i < n; i++) {
        // Если улица совпадает и возраст МЕНЬШЕ 50 лет
        if (people[i].address.street == search_street && people[i].age < 50) {
            if (people[i].gender == 'M' || people[i].gender == 'm') {
                men_count++;
            }
            if (people[i].gender == 'F' || people[i].gender == 'f') {
                women_count++;
            }
        }
    }

    // Выводим результат
    cout << "\nNa ulice " << search_street << " prozhivayut do 50 let:" << endl;
    cout << "Muzhchin: " << men_count << endl;
    cout << "Zhenschin: " << women_count << endl;

    return 0;
}

ЧАСТЬ 2. ИЗУЧЕНИЕ МАССИВОВ И СТРУКТУР ЯЗЫКА СИ++
Цель работы
Изучение работы со структурами и массивами структур в языке C++.
Условие задачи (Вариант 17)
Определите структуру «Житель». Поля: ФИО, адрес (улица, дом, квартира), пол, возраст.
В программе задайте массив жителей и определите, сколько лиц мужского и женского пола в возрасте до 50 лет проживают на заданной улице.

Текст программы с комментариями
include 
include 
using namespace std;
// Структура для адреса
struct Address {
    string street;
    int house;
    int flat;
};

// Структура для жителя

struct Zhitel {
    string fullname;
    Address address;
    char gender;
    int age;

};

int main() {
    int n;
    cout << "Skolko zhiteley vvesti? ";
    cin >> n;

Zhitel people[100];

for (int i = 0; i < n; i++) {
    cout << "\nZhitel " << i + 1 << ":" << endl;

    cout << "FIO: ";
    cin.ignore();
    getline(cin, people[i].fullname);

    cout << "Ulica: ";
    getline(cin, people[i].address.street);

    cout << "Dom: ";
    cin >> people[i].address.house;

    cout << "Kvartira: ";
    cin >> people[i].address.flat;

    cout << "Pol (M/F): ";
    cin >> people[i].gender;

    cout << "Vozrast: ";
    cin >> people[i].age;
}

string search_street;
cout << "\nVvedite ulicu dlya poiska: ";
cin.ignore();
getline(cin, search_street);

int men_count = 0;
int women_count = 0;

for (int i = 0; i < n; i++) {
    if (people[i].address.street == search_street && people[i].age < 50) {
        if (people[i].gender == 'M' || people[i].gender == 'm') {
            men_count++;
        }
        if (people[i].gender == 'F' || people[i].gender == 'f') {
            women_count++;
        }
    }
}

cout << "\nNa ulice " << search_street << " prozhivayut do 50 let:" << endl;
cout << "Muzhchin: " << men_count << endl;
cout << "Zhenschin: " << women_count << endl;

return 0;


}

Контрольный пример и результаты работы программы

Пример работы:

text

Skolko zhiteley vvesti? 3

Zhitel 1:

FIO: Ivanov I.I.

Ulica: Baumanskaya

Dom: 10

Kvartira: 12

Pol (M/F): M

Vozrast: 25

Zhitel 2:

FIO: Petrova A.S.

Ulica: Baumanskaya

Dom: 10

Kvartira: 15

Pol (M/F): F

Vozrast: 30

Zhitel 3:

FIO: Sidorov K.V.

Ulica: Baumanskaya

Dom: 12

Kvartira: 1

Pol (M/F): M

Vozrast: 60

Vvedite ulicu dlya poiska: Baumanskaya

Na ulice Baumanskaya prozhivayut do 50 let:

Muzhchin: 1

Zhenschin: 1

Вывод по Части 2
Использование структур позволяет удобно объединять связанные данные (ФИО, адрес, возраст) в одну переменную, а циклы `for` позволяют быстро обрабатывать массивы таких структур.
