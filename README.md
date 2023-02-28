# Домашнее задание к занятию "Выстраивание процесса непрерывной интеграции"

## Цель задания

1. Научиться настраивать CI на основе Github Actions

------

## Инструкция к заданию

1. Скачайте и установите профессиональный редактор кода [Intellij Idea Community Version](https://www.jetbrains.com/idea/download/)
1. Откройте IDEA и [создайте и настройте новый Maven-проект](QA_Maven_Idea_Create.md) (под каждую задачу следует создавать отдельный проект, если обратное не сказано в условии)
2. Создайте пустой репозиторий на GitHub и свяжите его с папкой вашего проекта (не с какой-либо другой папкой).
3. Правильно настройте репозиторий в плане `.gitignore`. Проигнорируйте папки `.idea` и `target` (раньше была `out`) и `.iml`-файл - их в репозитории быть не должно.
4. :new: Закоммитьте и запушьте созданный проект на гитхаб, [настройте Github Actions](QA_CI.md), сделайте `git pull`.
4. Выполните в IDEA требуемую задачу согласно условию.
5. Проверьте соблюдение [правил форматирования кода](QA_Java_Idea_Format.md)
6. :new: Убедитесь что при запуске `mvn clean verify` (раньше было `mvn clean test`) все тесты запускаются, проходят, а сборка завершается успешно
7. Закоммитьте и отправьте в репозиторий содержимое папки проекта.
8. :new: Убедитесь, что CI запустился на последнем коммите и завершился успешно (зелёная галочка).

------

## Материалы, которые пригодятся для выполнения задания

1. [Как создать Maven-проект в IDEA?](QA_Maven_Idea_Create.md)
1. [Как отформатировать код в Java?](QA_Java_Idea_Format.md)
1. :new: [Как настроить CI на основе Github Actions?](QA_CI.md)

------

## Задание 1 (обязательное)

Перед вами код сервисного класса:
```java
package ru.netology.statistic;

public class StatisticsService 
    public long findMax(long[] incomes) {
        long currentMax = incomes[0];
        for (long income : incomes) {
            if (currentMax < income) {
                currentMax = income;
            }
        }
        return currentMax;
    }
}
```

И код тест-класса, который его тестирует:
```java
package ru.netology.statistic;

import org.junit.jupiter.api.Test;

import org.junit.jupiter.api.Assertions;

public class StatisticsServiceTest {

  @Test
  void findMax() {
    StatisticsService service = new StatisticsService();

    long[] incomesInBillions = {12, 5, 8, 4, 5, 3, 8, 6, 11, 11, 12};
    long expected = 12;

    long actual = service.findMax(incomesInBillions);

    Assertions.assertEquals(expected, actual);
  }
}
```

Ваша задача состоит в том, чтобы:
1. Создать Maven-проект и поместить в него эти два класса;
2. Запустить `mvn clean test` и убедиться, что тесты проходят;
3. Создать публичный репозиторий и запушить в него проект;
4. Настроить CI на основе Github Actions, после чего не забыть сделать `git pull`;
5. Добавить в проект JaCoCo и настроить его в режиме обрушения сборки по недостаточному покрытию, а именно 100% покрытие по счётчику `BRANCH`;
6. Запустить `mvn clean verify` и убедиться, что сборка упадёт из-за недостаточного покрытия;
7. Проанализировать сгенерированный отчёт по покрытию, дописать недостающие тесты (сам же сервисный класс трогать нельзя!) для полного покрытия;
8. Сделать коммит и пуш, убедиться что сборка на гитхабе проходит

------
