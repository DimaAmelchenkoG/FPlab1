# FPlab1
- Выполнил: Амельченко Дмитрий Сергеевич
- Группа: P3332
- ИСУ: 336358
## Задача 8:
![image](https://github.com/user-attachments/assets/cf23b0c0-d27a-4e00-987b-4cadec38df18)

## Хвостовая рекурсия:
```
count_of_words(String) ->
  count_of_words(String, 0).

count_of_words([], Count) ->
  Count;

count_of_words([H | T], Count) ->
  NewCount = if
               H == $0 -> Count + 1;
               true -> Count
             end,
  count_of_words(T, NewCount).
```

## Рекурсия
```
len([]) -> 0;
len([_Head | Tail]) -> 1 + len(Tail).
```
## Должны использоваться функции reduce/fold, filter и аналогичные)
```
max_proizved(Number, Length, Max) ->
  Indexes = lists:seq(1, Length - 12),
  lists:foldl(
    fun(I, Acc) ->
    Substring = string:substr(Number, I, 13),
    Count = count_of_words(Substring),

    if Count == 0 ->
      ResultProizved = lists:foldl(
          % описание функции                                      | Acc | Список
          fun(Digit, Proizved) -> Proizved * (list_to_integer([Digit])) end, 1, Substring),
        max(Acc, ResultProizved);
      true ->
        Acc
    end
              end, Max, Indexes).
```

## генерация последовательности при помощи отображения (map)
```
max_proizved(Number, Length, Max) ->
  Indexes = lists:seq(1, Length - 12),
  lists:foldl(
    fun(I, Acc) ->
      Substring = string:substr(Number, I, 13),
      Count = count_of_words(Substring),

      if Count == 0 ->
        GoToInteger = fun(Sym) -> list_to_integer([Sym]) end,
        SubstringLikeInteger = lists:map(GoToInteger, Substring),
        ResultProizved = lists:foldl(
          % описание функции                                      | Acc | Список
          fun(Digit, Proizved) -> Proizved * Digit end, 1, SubstringLikeInteger),

        max(Acc, ResultProizved);
        true ->
          Acc
      end
    end, Max, Indexes).
```

## Вывод
В ходе выполнения данной лабораторной работы, я познакомился с таким языком программирования как Erlang. Я изучил его синтаксис и некоторые инструменты.
Я познакомился с такими инструментами, как:
- Хвостовая рекурсия
- reduce/fold, filter, map
- Генераторы последовательностей
- Pattern matching
Я впервые писал на функциональном языке программирования и сделал сделующие выводы: писать на Erlang намного проще, в плане работа с данными происходит гораздо компактней и гибко.
Сверстки, фильтры и отображения очень сильно упращают нам жизнь. Отдельно выделю хвостовую рекурсию, очень понравилось, как мы защищаем стэк от переполнения
