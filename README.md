# rides-minimal

Основной файл: [rides_minimal.ipynb](https://github.com/epogrebnyak/rides-minimal/blob/master/rides_minimal.ipynb)

## Цели

- [ ] Переносим сюда оставшийся код из [ноутбука rides2.ipynb на Google Colab](https://colab.research.google.com/drive/1DXsJBTyVvAXrU1aEy5GFWiF_i75LmWS1#scrollTo=h3WG4Nex_pmC)
- [ ] Составляем roadmap доработок (вставки из "тяжелого" алгоритма и т.д.)


## Roadmap доработок 

- [ ] Попробовать [nbdev](https://github.com/fastai/nbdev)
- [ ] Перенести / доработать графику (особ. - начало и конец треков)

Из "тяжелого" алгоритма:

- [ ] Функция пути по времени

## Сделано

- [x] Новый показатель перекрытия с учетом длины общего пути `overlap` 
- [x] Вывешиваем минимальный пример использования пакета на Colab 
- [x] Открыл репозитарий для работы с Colab
- [x] Переносим сюда анализ датасета [one_day.zip](one_day.zip)

## Not todo
- [ ] Генерируем документацию (sphinx или mkdocs-react) - nbdev
- [ ] Пишем тесты на основе еще более короткого датасета, чем [one_day.zip](one_day.zip)


## Псеводкод обработки данных

### Вне репо:

- Мы прочли сырые данные из JSON, получили одну таблицу данных, запаковали в `one_day.zip`

В этом репо:

- Сохранили локально исходные данные `one_day.zip`
- Преобразовали исходные данные в список треков `[Route: pd.DataFrame]`
- Составляем все возможные пары треков, количество таких пар будет равно `n * (n-1) / 2`
- Проводим анализ фигур треков в два этапа:
  - выбраковываем непересекающиеся треки (в грубой апроксимации треков)
  - оцениваем близость фигур оставшихся пар треков треков (в более точной апрокимации треков)
- Внутри каждой пары треков получаем два коэффициента перекрытия треков (первого трека вторым, второго трека первым)
- Добавляем данные о длине треков, рассчитываем дополнительный коэффициент перекрытия с учетом длины
- Сделали выгрузку `output.csv` - должен совпадать с top 20 в ноутбуке

После этого репо:

- Анализируем все попарные характеристики, получаем сводные результаты на уровне всей выборки

## Гипотезы и упрощения

- смотрим путь машины внутри суток без учета разных заказов (объединяем заказы в один в течение суток)

## Идеи и ключевые слова

Расстояния между кривыми:

- Hausdorff distance
- Fréchet distance
