========================
**ECOS Артефакты**
========================

Определения
~~~~~~~~~~~

**Артефакт** - единица расширения системы. Примеры артефактов: :guilabel:`Тип`, :guilabel:`Форма`, :guilabel:`Журнал`.

Переопределение артефактов
~~~~~~~~~~~~~~~~~~~~~~~~~~

Для переопределения артефактов можно создать папку с именем override в корне директории с артефактами.

Пример структуры папок::

  eapps:
    - artifacts:
        - ui:
            - form:
                - some-form.json
            - journal:
                - some-journal.yml
        - override:
            - ui:
                - form:
                    - some-form.json

Для формы some-form.json будет создан патч с типом override и порядком -100 (по умолчанию). Если требуется настроить порядок,
то следует в корне папки override создать файл ``meta.yml``. В нем возможны следующие настройки:

.. list-table:: Список возможных настроек в override/meta.yml
    :header-rows: 1

    *   - Название
        - Тип данных
        - Описание
    *   - order
        - float
        - Порядок патча для перезаписи артефакта. Сначала применяются патчи с меньшим порядком.
    *   - scope
        - string
        - | Параметр служит для исключения коллизий идентификаторов override патчей.
          | Идентификатор патча формируется по следующему шаблону: override[_{{scope}}]$ui/form$some-form

**Особенности**

1. Перезапись артефактов работает вне зависимости от того откуда деплоится основной артефакт
