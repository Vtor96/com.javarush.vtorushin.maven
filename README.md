# Racer Game - сборка JavaFX-игры через Maven

Учебный проект для курса JavaRush (модуль «Java Professional»). 
Задача — настроить сборку исполняемого fat-JAR-файла с JavaFX-игрой (гонка) и локальным игровым движком. 
Весь игровой код предоставлен JavaRush, основная работа — конфигурация Maven.

## Что сделано

- Настроен `pom.xml` с 4 зависимостями: commons-lang3, javafx-controls, desktop-game-engine (локальная), junit-jupiter-engine (test).
- Локальная зависимость `desktop-game-engine` устанавливается из папки `lib/` через `maven-install-plugin` на фазе `validate`.
- Зависимости копируются в `target/lib/` через `maven-dependency-plugin`.
- Собирается fat-JAR через `maven-jar-plugin` с манифестом:
  - `Main-Class` — `JarRsrcLoader` (загрузчик из Eclipse JDT для запуска JavaFX из JAR с вложенными зависимостями).
  - `Rsrc-Main-Class` — `com.javarush.games.racer.RacerGame`.
  - `Class-Path` — путь к вложенным JAR-зависимостям.
- Тест `StrangeTest` исключён из сборки через `maven-surefire-plugin`.
- Секция `resources` упаковывает JAR-зависимости внутрь финального архива в папку `lib/`.

## Стек

- Java 18
- JavaFX 18.0.1
- Maven 3
- JUnit 5 (тесты)
- JavaRush Desktop Game Engine (локальный JAR)

## Требования

- JDK 18.0.1
- Maven 3.6+

##  Результат
target/project-maven-1.0.jar (fat-JAR со всеми зависимостями внутри).

## Как собрать

```bash
mvn clean install 
