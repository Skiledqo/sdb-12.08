# Домашнее задание к занятию «Резервное копирование баз данных» - Иван Серебренников

## Задание 1

Кейс
Финансовая компания решила увеличить надёжность работы баз данных и их резервного копирования.

Необходимо описать, какие варианты резервного копирования подходят в случаях:

1.1. Необходимо восстанавливать данные в полном объёме за предыдущий день.

1.2. Необходимо восстанавливать данные за час до предполагаемой поломки.

1.3.* Возможен ли кейс, когда при поломке базы происходило моментальное переключение на работающую или починенную базу данных.

Приведите ответ в свободной форме.

**ОТВЕТ:** 

1.1. Для восстановления данных в полном объеме за предыдущий день наиболее подходящим вариантом резервного копирования является ежедневное создание полных резервных копий базы данных. Это означает, что каждый день в конце рабочего дня создается копия всех данных, которая сохраняется на отдельном носителе (например, на удаленном сервере или в облачном хранилище). В случае потери данных, можно будет восстановить базу данных из последней полной резервной копии за предыдущий день.

1.2. Для восстановления данных за час до предполагаемой поломки требуется более частое создание резервных копий. Здесь подходят инкрементальные или дифференциальные резервные копии. С инкрементальными копиями создаются резервные копии только измененных данных с момента предыдущей копии. С дифференциальными копиями создаются резервные копии всех измененных данных с момента последней полной копии. Это позволяет восстанавливать данные на более близкий момент времени.

1.3. Для моментального переключения на работающую или починенную базу данных требуется использовать методы высокой доступности (High Availability, HA) и репликации данных. В данном случае, можно рассмотреть кластеризацию баз данных, где имеется несколько идентичных узлов (например, мастер-мастер репликация), и при поломке одного из узлов система автоматически переключается на работающий узел. Это обеспечивает непрерывную работу системы и минимальное время простоя в случае сбоя. Также, использование облачных решений для автоматической масштабируемости и управления ресурсами может быть важным аспектом для обеспечения надежности и моментального переключения в случае поломки.

## Задание 2

2.1. С помощью официальной документации приведите пример команды резервирования данных и восстановления БД (pgdump/pgrestore).

2.1.* Возможно ли автоматизировать этот процесс? Если да, то как?

Приведите ответ в свободной форме.

**ОТВЕТ:**

2.1. Для резервирования и восстановления данных в PostgreSQL можно использовать утилиты pg_dump и pg_restore. Ниже представлены примеры команд для резервирования и восстановления базы данных:

Резервирование БД:
**pg_dump -U <пользователь> -d <имя_базы_данных> -f <путь_к_файлу_резервной_копии>**

**pg_dump -U myuser -d mydatabase -f backup.sql**


Восстановление БД:

**pg_restore -U <пользователь> -d <имя_базы_данных> <путь_к_файлу_резервной_копии>**

**pg_restore -U myuser -d mydatabase backup.sql**

## Задание 3

3.1. С помощью официальной документации приведите пример команды инкрементного резервного копирования базы данных MySQL.

3.1.* В каких случаях использование реплики будет давать преимущество по сравнению с обычным резервным копированием?

**Ответ:**

3.1 Для инкрементного резервного копирования базы данных MySQL можно использовать утилиту mysqldump с параметрами, позволяющими создавать резервные копии только измененных данных. Пример команды для инкрементного резервного копирования может выглядеть следующим образом:

**mysqldump -u <пользователь> -p<пароль> --single-transaction --databases <имя_базы_данных> > <путь_к_файлу_резервной_копии>**

3.1* Использование реплики базы данных может дать следующие преимущества по сравнению с обычным резервным копированием:

Непрерывность работы: Репликация позволяет иметь актуальную реплику данных, которая всегда синхронизирована с мастер-сервером. Это обеспечивает непрерывную доступность к данным даже в случае сбоя на мастер-сервере.

Снижение нагрузки: Резервное копирование базы данных может быть ресурсоемким процессом, особенно для больших баз данных. Используя реплику для создания резервных копий, можно снизить нагрузку на мастер-сервер и обеспечить более высокую производительность.

Быстрое восстановление: В случае сбоя на мастер-сервере, можно быстро переключиться на реплику и продолжить работу. Это сокращает время простоя и минимизирует потерю данных.

Тестирование обновлений: Репликация позволяет тестировать обновления и изменения в стабильной среде перед их применением к мастер-серверу.

Распределенная нагрузка: Репликация может использоваться для распределения нагрузки между мастером и одной или несколькими репликами, что увеличивает производительность системы.

Однако репликация также требует дополнительной настройки и управления, и может быть более сложной для поддержки по сравнению с обычным резервным копированием. Выбор между репликацией и обычным резервным копированием зависит от конкретных требований и характеристик системы.




