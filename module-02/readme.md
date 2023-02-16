# Домашнее задание для [Модуля 02: Базы данных и SQL](https://github.com/Data-Learn/data-engineering/blob/master/DE-101%20Modules/Module02/readme.md)


## :ledger: Cкрипт загрузки данных и создания таблиц
- [Технологический стек](#технологический-стек)
- [Реализованные проверки](#реализованные-проверки)
- [Сборка в Jenkins](#сборка-в-jenkins)
- [Запуск тестов](#запуск-тестов)
- [Allure отчет](#allure-отчет)
- [Уведомления в Telegram с использованием бота](#уведомления-в-telegram-с-использованием-бота)
- [Пример запуска теста в Selenoid](#пример-запуска-теста-в-selenoid)



## :heavy_check_mark: Технологический стек <a name="технологический-стек"></a>
<p align="center">
<a href="https://www.jetbrains.com/idea/"><img src="/images/Intelij_IDEA.svg" width="50" height="50"  alt="IDEA"/></a>
<a href="https://www.java.com/"><img src="/images/Java.svg" width="50" height="50"  alt="Java"/></a>
<a href="https://github.com/"><img src="/images/Github.svg" width="50" height="50"  alt="Github"/></a>
<a href="https://junit.org/junit5/"><img src="/images/JUnit5.svg" width="50" height="50"  alt="JUnit 5"/></a>
<a href="https://gradle.org/"><img src="/images/Gradle.svg" width="50" height="50"  alt="Gradle"/></a>
<a href="https://selenide.org/"><img src="/images/Selenide.svg" width="50" height="50"  alt="Selenide"/></a>
<a href="https://aerokube.com/selenoid/"><img src="/images/Selenoid.svg" width="50" height="50"  alt="Selenoid"/></a>
<a href="https://github.com/allure-framework/allure2"><img src="/images/Allure_Report.svg" width="50" height="50"  alt="Allure"/></a>
<a href="https://www.jenkins.io/"><img src="/images/Jenkins.svg" width="50" height="50"  alt="Jenkins"/></a>
<a href="https://telegram.org/"><img src="/images/Telegram.svg" width="50" height="50"  alt="Telegram"/></a>  
</p>

## :heavy_check_mark: Реализованные проверки <a name="реализованные-проверки"></a>
- Проверка работы основного меню страницы
- Проверка наличия вакансии QA auto
- Проверка заполнения формы обратной связи
- Проверка работы ссылки на Телеграм-канал

## :heavy_check_mark: [Сборка](https://jenkins.autotests.cloud/job/012-lenabodrenok-mobileup_tests/) в Jenkins <a name="сборка-в-jenkins"></a>
### &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Основная информация  
<p align="center">
<img title="Jenkins Dashboard" src="/images/Jenkins_main.png">
</p>

### &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Выбор параметров сборки  
<p align="center">
<img title="Jenkins Build" src="/images/Jenkins_parameters.png">    
</p>

## :heavy_check_mark: Запуск тестов <a name="запуск-тестов"></a>
- [x] Локальный запуск тестов:
```
gradle clean test
```
- [x] Удаленный запуск тестов:
```
clean
test
-Dbrowser=${BROWSER}
-DbrowserVersion=${BROWSER_VERSION}
-DbrowserSize=${BROWSER_SIZE}
-DbaseUrl=${BASE_URL}
-DselenoidUrl=${REMOTE}
```

## :heavy_check_mark: Allure отчет <a name="allure-отчет"></a>
### &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Главный экран отчета  
<p align="center">
<img title="Allure Owerview" src="/images/Allure Report_main.png">
</p>

### &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Страница с проведенными тестами  
<p align="center">
<img title="Allure Suites" src="/images/Allure Report_suites.png">
</p>

## :heavy_check_mark: Уведомления в Telegram с использованием бота <a name="уведомления-в-telegram-с-использованием-бота"></a>
<p align="center">
<img title="Telegram Bot" src="/images/Telegram_bot.jpg">
</p>

## :heavy_check_mark: Пример запуска теста в Selenoid <a name="пример-запуска-теста-в-selenoid"></a>
<p align="center">
<img title="Selenoid Video" src="/images/attach-video.gif">
</p>

