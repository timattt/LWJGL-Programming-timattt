# LWJGL game-dev
В этом репозитории располагается мой самый большой game-dev проект.  
The chapter - пошаговая стратегия по своим механикам похожая на серию игр Civilization и Humankind.
### Код разделен на 3 части:
* движок (оболочка над LWJGL с удобной системой создания объектов, прорисовкой, управления системными объектами и т.д.)
* The chapter (собственно сама игра, для работы необходимо подключить движок)
* Тестовый сценарий (код для отдельного jar файла со всеми ресурсами и настройками для игры)

### Необходимые библиотеки
* joml (версия ниже 1.10)
* lwjgl
* assimp
* glfw
* nanovg
* openal
* opengl
* stb

Все вышеперечисленное можно скачать [тут](https://www.lwjgl.org/).

# The chapter
Теперь подробнее о самой игре.
Итак, у нас есть карта - разделенные на клетки, на каждой клетке может что-нибудь находится: город, отряд солдат, элемент ландшафта.   
Игроки делают свой ход по очереди. Во время своего хода можно двигать свои армии на фиксированное колличество клеток, устраивать сражения с соперником и т.д.
Главное мысль, которой я придерживался при разработке - универсальность кода, т.е. возможность быстро и эффективно добавлять любые нововведения в игру. Для этого разработана система
сценариев, о ней далее.

# Основные игровые механики
## Юниты
Юнит - это группа "людей", которых игрок может двигать по карте и выполнять с их помощью различные действия. Например, отряд стрелков считается одним юнитом.   
**Вот юнит игрока выделен, красным отмечен радиус стрельбы**
  ![](https://github.com/timattt/LWJGL-Programming-timattt/blob/master/imgs/Unit_example2.png)
Теперь посмотрим, что могут делать юниты.   
**Тут юнит двигается**
  ![](https://github.com/timattt/LWJGL-Programming-timattt/blob/master/imgs/Unit_example3.png)
**А тут два юнита перестреливаются**
  ![](https://github.com/timattt/LWJGL-Programming-timattt/blob/master/imgs/Unit_example4.png)
**Здесь видна анимация у юнита сразу после сражения**
  ![](https://github.com/timattt/LWJGL-Programming-timattt/blob/master/imgs/Unit_example5.png)
До этого мы видели юнит линейной пехоты, он пренадлежит к классу стрелков, но есть еще и юниты ближнего боя, посмотрим их.   
**А вот юнит ближнего боя - мечник**
  ![](https://github.com/timattt/LWJGL-Programming-timattt/blob/master/imgs/Unit_example6.png)
**Кстати, можно легко менять колличество человечков, которые отображаются**
  ![](https://github.com/timattt/LWJGL-Programming-timattt/blob/master/imgs/Unit_example7.png)
**А вот большая баталия**
  ![](https://github.com/timattt/LWJGL-Programming-timattt/blob/master/imgs/Unit_example8.png)
## Ландшафт
Помимо ровной карты можно сделать холмистую, гористую и вообще какую мы захотим, ибо есть встроенная система height-map. И колличество полигонов в одной клетке регулируется. А также можно установить цвет или комбинацию цветов для карты.     
**Пейзаж 1**
  ![](https://github.com/timattt/LWJGL-Programming-timattt/blob/master/imgs/Terrain_example1.png)
  Теперь больше будет полигонов.   
**Пейзаж 2**
  ![](https://github.com/timattt/LWJGL-Programming-timattt/blob/master/imgs/Terrain_example2.png)
Включим цветовую интерполяцию.   
**Пейзаж 3**
  ![](https://github.com/timattt/LWJGL-Programming-timattt/blob/master/imgs/Terrain_example3.png)

## Сценарии
Сценарий состоит из генератора карты, объектов на карте, набора игровых правил.
Т.е. сама игра по умолчанию никакого игрового контента не имеет (кроме нескольких основных механик), все лежит в сценарии.
При запуске игры вам предлагается выбрать сценарий, который лежит упакованный в jar-файл, таким образом игрок может по своему желанию подгрузить то, что захочет.
Но главное система сценариев дает неограниченные возможности игровому сообществу для моддинга, любой человек сможет добавить в игру все, что захочет.
Это прямо как моды для minecraft, только не нужно устанавливать никакого стороннего ПО (вроде forge), все легко, доступно и удобно.   

## WIP
[Тут](https://github.com/timattt/LWJGL-Programming-timattt/blob/master/WIP.md) можно посмотреть игровые механики, которые сейчас находятся на ранней стадии разработки.

# Иерархии сущностей
Далее представленны несколько диаграмм, на которых показаны связи различных внутриигровых объектов. Для какждого элемента диаграммы в коде есть соответствующие
инструменты для обработки и добавления. Так что для создания нового контента вам достаточно унаследовать свой класс от нужного.

* TileObject (объекты, которые расположены на карте)
 ![](https://github.com/timattt/LWJGL-Programming-timattt/blob/master/imgs/TileObjectStructure.png)

