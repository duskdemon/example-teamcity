#devops-netology
### 09-ci-05-teamcity
# Домашнее задание к занятию "09.05 Teamcity"

## Подготовка к выполнению

1. В Ya.Cloud создайте новый инстанс (4CPU4RAM) на основе образа `jetbrains/teamcity-server`
2. Дождитесь запуска teamcity, выполните первоначальную настройку
3. Создайте ещё один инстанс(2CPU4RAM) на основе образа `jetbrains/teamcity-agent`. Пропишите к нему переменную окружения `SERVER_URL: "http://<teamcity_url>:8111"`
4. Авторизуйте агент
5. Сделайте fork [репозитория](https://github.com/aragastmatb/example-teamcity)
6. Создать VM (2CPU4RAM) и запустить [playbook](./infrastracture)
**Выполнение**  
скриншот с созданными ВМ в яндекс клауде:
![скрин YC](https://github.com/duskdemon/example-teamcity/blob/main/prep01.png)
## Основная часть

1. Создайте новый проект в teamcity на основе fork
2. Сделайте autodetect конфигурации
3. Сохраните необходимые шаги, запустите первую сборку master'a
 **Выполнение**  
скриншот с логом первого билда:
![скрин билда](https://github.com/duskdemon/example-teamcity/blob/main/build01.png)  
4. Поменяйте условия сборки: если сборка по ветке `master`, то должен происходит `mvn clean deploy`, иначе `mvn clean test`
5. Для deploy будет необходимо загрузить [settings.xml](./teamcity/settings.xml) в набор конфигураций maven у teamcity, предварительно записав туда креды для подключения к nexus
6. В pom.xml необходимо поменять ссылки на репозиторий и nexus
7. Запустите сборку по master, убедитесь что всё прошло успешно, артефакт появился в nexus
 **Выполнение**  
скриншоты с логом билда и артефакта в нексусе:
![скрин билда 2](https://github.com/duskdemon/example-teamcity/blob/main/build02.png)  
![скрин нексус](https://github.com/duskdemon/example-teamcity/blob/main/nexus01.png)  
8. Мигрируйте `build configuration` в репозиторий
9. Создайте отдельную ветку `feature/add_reply` в репозитории
10. Напишите новый метод для класса Welcomer: метод должен возвращать произвольную реплику, содержащую слово `hunter`
11. Дополните тест для нового метода на поиск слова `hunter` в новой реплике
12. Сделайте push всех изменений в новую ветку в репозиторий
13. Убедитесь что сборка самостоятельно запустилась, тесты прошли успешно
 **Выполнение**  
сборка самостоятельно запустилась, тесты прошли успешно:
![скрин билда 3](https://github.com/duskdemon/example-teamcity/blob/main/build03.png)  
14. Внесите изменения из произвольной ветки `feature/add_reply` в `master` через `Merge`
15. Убедитесь, что нет собранного артефакта в сборке по ветке `master`
16. Настройте конфигурацию так, чтобы она собирала `.jar` в артефакты сборки
17. Проведите повторную сборку мастера, убедитесь, что сбора прошла успешно и артефакты собраны
 **Выполнение**  
получилось:  
![скрин билда 4](https://github.com/duskdemon/example-teamcity/blob/main/build04.png)  
18. Проверьте, что конфигурация в репозитории содержит все настройки конфигурации из teamcity
19. В ответ предоставьте ссылку на репозиторий
 **Выполнение**  
[Ссылка]https://github.com/duskdemon/example-teamcity/blob/main/README.md

## Доработка:
**Спасибо за работу, не вижу настройки проекта в виде кода (шаг 8 основной части)**
 **Выполнение**

Настройка производится в веб-интерфейсе через Administration - Example Teamcity - Versionized settings
Создаем/выбираем vcs root, вводим URL и учетные данные для доступа, нажимаем "apply". Далее делаем необходимые настройки синхронизации.
![скрин vcs](https://github.com/duskdemon/example-teamcity/blob/main/fix01.png)
