Описание проекта "Tower Defense Game"
Проект является реализацией игры в жанре "Tower Defense", где игроку предстоит защищать базу от волн врагов, расставляя
башни. На данный момент реализован базовый функционал: можно выиграть если пережить три волны, или проиграть если хотя 
бы один враг дойдёт. Также есть два типа башен, переключение между ними по клавишам 1 и 2.
Позиции для расположения башен видны всегда, что сильно ухудшает впечатление от интерфейса. Также заложена основа системы
апгрейдов, но их самих нет.

Описание проекта:
main.py - главный файл, содержащий основной игровой цикл, обработку событий, обновление состояний игры и отрисовку 
элементов игры.

settings.py - файл настроек, содержит параметры конфигурации игры, такие как размеры экрана, стоимость и параметры башен,
пути к ресурсам и т.д.

level.py - содержит логику уровня, управление волнами врагов, их спавн, а также расстановку башен и обработку коллизий.

grid.py - отвечает за управление сеткой, на которой игрок может размещать башни, проверку на доступность места для 
размещения башни.

tower.py – базовый класс башни и его наследники для разных типов башен, содержит логику стрельбы, поиска цели и улучшения.

enemy.py - определяет класс врага, его движение по карте, здоровье и получение урона.

bullet.py - класс пули, управляет движением пули, проверкой попаданий в врагов и нанесением урона.

Более подробно о файлах:
main.py

class TowerDefenseGame: Главный класс игры, управляющий основным циклом игры, событиями, обновлениями состояний и отрисовкой.
__init__(self): Конструктор, инициализирует основные параметры игры, загружает ресурсы и создаёт объекты уровня и сетки.
game_over(self): Обрабатывает условия окончания игры.
is_position_inside(self, pos): Проверяет, находится ли позиция в пределах игрового поля.
_check_events(self): Обрабатывает игровые события, такие как нажатие клавиш и клики мыши.
_update_game(self): Обновляет состояние игры, вызывая обновления уровня и сетки.
_draw_win_screen(self): Отображает экран победы.
_draw_game_over_screen(self): Отображает экран проигрыша.
_draw(self): Управляет отрисовкой всех элементов игры.
run_game(self): Запускает основной игровой цикл.

level.py

class Level: Управляет уровнем игры, волнами врагов и расстановкой башен.
__init__(self, game): Инициализирует уровень игры.
start_next_wave(self): Запускает следующую волну врагов.
spawn_next_enemy(self): Генерирует следующего врага текущей волны.
attempt_place_tower(self, mouse_pos, tower_type): Пытается разместить башню выбранного типа в позиции курсора.
update(self): Обновляет состояние уровня, врагов, башен и пуль.
draw_path(self, screen): Отображает путь врагов.
draw(self, screen): Отрисовывает уровень, включая врагов, башни и пули.

grid.py

class Grid: Отвечает за сетку, где игрок может размещать башни.
__init__(self, game): Инициализирует сетку.
update(self): Может использоваться для обновления сетки.
draw(self): Отображает сетку на экране.
place_tower(self, tower): Размещает башню на сетке.
remove_tower(self, tower): Удаляет башню с сетки.
get_grid_position(self, mouse_pos): Возвращает позицию сетки, ближайшую к позиции курсора.
is_spot_available(self, grid_pos): Проверяет, доступно ли место для размещения башни.

tower.py

class Tower: Базовый класс для всех башен, его методы включают инициализацию, отрисовку, обновление, стрельбу, поворот 
к цели и поиск цели.
class BasicTower(Tower) и class SniperTower(Tower): Конкретные реализации башен, расширяющие базовый класс. Снайперская 
имеет собственный алгоритм выбора цели.
 
Внесённые изменения:
В main.py добавлено условие: сетка для установления башни появляется при нажатии на "Пробел" - переключатель положения:

![Image alt](https://github.com/GaGaGaGala/Tower-Defense-Game/blob/master/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%20(452).png)
показать сетку и не показать сетку.

![Image alt](https://github.com/GaGaGaGala/Tower-Defense-Game/blob/master/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%20(451).png)
