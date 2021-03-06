# Контентные блоки

Контентные блоки используются для избежания дублирования повторяющихся блоков или элементов в контенте или представлениях сайта.

> Аналогичный функционал в MODX называется чанками(chunks), а в WordPress - шорткодами(shortcodes).

## Определение блока

Для определения контентного блока - создайте соответствующую запись в разделе "Контентные блоки" панели администрирования:

- **Название** - используется для визуальной идентификации блока
- **Ключ** - тот ключ, по которому будет вызываться этот блок внутри контента
- **Значение** - собственно то, на что будет заменяться оператор вызова контентного блока непосредственно в контенте
- **Предварительная загрузка** - этот блок контента будет загружаться при каждом запросе к сайту. Включите эту опцию для наиболее часто используемых блоков.

Контентный блок может принимать дополнительные параметры, например:

```
Это простой блок, который сейчас выведет отформатированный параметр
[[+paramName:format,format_attribute1,'format_attribute_n']].
А здесь мы просто выведем значение параметра как есть [[+anotherParam]].
```

Здесь:

- **paramName** - название параметра(именно это название нужно будет передавать вместе соператором вызова блока). Плюс перед названием параметра обязателен.
- **format** - функция форматирования(опционально)
- **format_attribute1** и **format_attribute_n** - произвольное количество значений параметров, которые будут передаваться функции форматирования. Разделитель - запятая. Если значение в ковычках - оно трактуется как строка(string), без ковычек - как число с плавающей точкой(float).
- **[[+anotherParam]]** - название параметра. В данном примере он выводится "как есть".

## Использование контентного блока

В контенте вставляете оператор вызова блока, который имеет следующий формат:

```
[[$contentBlockKey paramName='paramValue' anotherParam=3.14]]
```
Здесь:
- **contentBlockKey** - замените на ключ вашего контентного блока. **Важно:** знак доллара перед ключем обязателен.
- **paramName** - название параметра
- **paramValue** - значение параметра. Если оно в одинарных ковычках - трактуется как строка(string). Иначе - как число с плавающуй точкой(float).

## Использование контентного блока в шаблоне

Для контентных блоков, не принимающих параметров, также возможно использование внутри шаблонов и представлений.

Для этого необходимо вызвать хелпер-функцию в view-файле:

``` php
<?= \app\modules\core\helpers\ContentBlockHelper::fetchChunkByKey('YOUR_BLOCK_KEY') ?>
```

