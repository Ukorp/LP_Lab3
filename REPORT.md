#№ Отчет по лабораторной работе №3
## по курсу "Логическое программирование"

## Решение задач методом поиска в пространстве состояний

### студент: Иванопуло А.Б.

## Результат проверки

| Преподаватель     | Дата         |  Оценка       |
|-------------------|--------------|---------------|
| Сошников Д.В. |              |               |
| Левинская М.А.|              |               |

> *Комментарии проверяющих (обратите внимание, что более подробные комментарии возможны непосредственно в репозитории по тексту программы)*


## Введение

Какие задачи удобным образом решаются методом поиска в пространстве состояний? 
Почему Prolog оказывается удобным языком для решения таких задач?

## Задание

Перенесите сюда условие задачи - это упростит проверку и чтение отчета.

## Принцип решения

Опишите своими словами принцип решения задачи, приведите важные фрагменты кода. Какие алгоритмы поиска вы использовали? 

## Результаты

% Поиск в глубину
depth([X|T], X, [X|T]).
depth(From, To, Way):-
    extend(From, Tmp), depth(Tmp, To, Way).

search_depth(From, To):-
    depth([From], To, Way), result(Way).

search_depth_time(From, To):-
    get_time(S1), depth([From], To, Way), get_time(F1),
    T1 is F1 - S1, write('Время: '), write(T1), nl.

% Поиск в ширину
breadth([[To|Way]|_], To, [To|Way]).
breadth([FirstWay|QI], To, Way):-
    findall(OtherWay, extend(FirstWay, OtherWay), PossibleWays),
    append(QI, PossibleWays, QO), !, breadth(QO, To, Way).
breadth([_|Other], To, Way):- breadth(Other, To, Way).

search_breadth(From, To):-
    breadth([[From]], To, Way), result(Way).

search_breadth_time(From, To):-
    get_time(S2), breadth([[From]], To, Way), get_time(F2),
    T2 is F2 - S2, write('Время: '), write(T2), nl.

% Поиск с итерационным заглублением
depth_limit([To|T], To, [To|T], _).
depth_limit(Way, To, Res, N):- N > 0,
    extend(Way, NewWay), N1 is N - 1,
    depth_limit(NewWay, To, Res, N1).

search_limit(From, To, Way, Limit):-
    depth_limit([From], To, Res, Limit).

integer(1).
integer(M):- integer(N), M is N + 1.

search_limit_time(From, To):-
    get_time(S3),
    integer(Lvl),
    search_limit(From, To, Way, Lvl),
    get_time(F3), T3 is F3 - S3,
    write('Время: '), write(T3), nl.

! Алгоритм поиска |  Длина найденного первым пути  |  Время работы  |
|-------------------------------------------------------------------|
| В глубину       |                                |                |
| В ширину        |                                |                |
| ID              |                                |                |

## Выводы

Сформулируйте *содержательные* выводы по лабораторной работе. 
Чему она вас научила? Над чем заставила задуматься? 

Какие алгоритмы поиска в каких случаях удобно использовать? Какие оказались оптимальными в вашем конкретном случае?

Помните, что несодержательные выводы -
самая частая причина снижения оценки за лабораторную.




