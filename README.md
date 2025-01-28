#include <iostream>
class CameraSizer // Создаем класс
{
    public:
    CameraSizer() : D(1.0/0.035) {} //конструктор по условию фокусное расстояние по умолчанию 35мм
    CameraSizer(double d) : D(d) {}  // Когда вызываем контруктор вызывает первый
    // Публичная функция
    double ReadD() { return D; } // метод ReadD для ввода оптической силы в диоптриях
    double Distance(double d)   // создаем функцию distanse расстояни до фотографируемого предмета
    {
      const double F = 1 / D;
      return ((d * F) / (d - F)); // расстояние от объектива
    }

   private: double D; //непубличный элемент D для хранения (приватный элемент)
    };

   int main()
    {
    double d;
    std::cout << "D = "; // Ввод элемента с клавиатуры
    if (!(std::cin >> d)) return 1; // Если не число; то вернуть 1, показать ОШИБКА

   CameraSizer def; // Переменная этого типа
   CameraSizer user(d);

   const double defFF = 2.0 / def.ReadD();
   const double userFF = 2.0 / user.ReadD();
   while (true)
   {
     std::cout << "d = ";
     // если d не число, то вернет значение 2

   if (d < defFF || d < userFF)
         {
            std::cout << "oshibka";
        }
        else
        {
            std::cout
            << "CCD distance = " << def.Distance(d)*1000 << std::endl
            << "OBJECT distance = " << user.Distance(d)*1000<< std::endl; // расстояние от объектива до объекта
            return 0;
        }
    }
}
