# django-yamaps
Интеграция Django и Яндекс.Карт.

Highly inspired by [django-address](https://github.com/furious-luke/django-address).

Тестировали на Python 3.5 и Django >= 1.9.


# Обновление с предыдущих версий

В предыдущих версиях `django-yamaps` содержали модели адресов, чтобы
можно было быстро начать разработку. В текущей версии они были удалены.

Точнее, перемещены в демку `example` вместе с `AddressField`.
`django-yamaps` теперь предоставляет только виджет для форм и
тэги для подключения Яндекс.Карт в Django-шаблоны.


# Widget

> Можно кликнуть по карте - адрес будет обновлен.

Виджет сохраняет данные, полученные от Яндекс.Карт, вместе с координатами
(широта и долгота) и "сырым" представлением.

Можно написать свое поле, чтобы перегнать данные из Яндекс.Карт в
свою модель адреса.

Django передает в виджет PK адреса в базе данных, так что Вы можете
указать в настройках модель адреса, чтобы виджет мог отобразить Ваши данные:

```python
YAMAPS_ADDRESS_MODEL = "app.Address"
```

(так же, как и с `USER_MODEL`).

Помимо этого на модели должен быть определен метод `to_raw` - если его
нет, будет использовано приведение к строке (`__str__`).

Примеры использования в папке `example`.


# Template tag

Для отображения карты с адресом подключите в шаблон библиотеку `yamaps`,
после чего укажите, куда в шаблоне поместить карту с помощью тэга
`yamaps`, а затем инициализировать Яндекс.Карты с помощью тэга
`yamaps_init`

```
{% load yamaps %}
{% yamaps address1 %}
{% yamaps address2 %}
...
{% yamaps addressN %}

{% yamaps_init %}
```

Вы можете указать стили карты вторым аргументом:

```
{% yamaps address "width: 640px; height: 480px;" %}
```
