---
title: "Singleton"
excerpt_separator: "<!--more-->"
categories:
  - Design patterns
tags:
  - design patterns
  - creational design patterns
---

Wzorzec kreacyjny dzieki któremu możesz być pewny, że istnieje tylko pojedyńcza instancja danej klasy.
Zapewnia również dostęp do tej instancji w zakresie całej aplikacji.

<!--more-->

Singleton łamie zasade pojedyńczej odpowiedzialności rozwiązując dwa problemy jednocześnie:

  1. Zapewnia istnienie tylko jednej instancji danej klasy.

  Częstym powodem dla którego chcemy aby istniała tylko jedna instancja jest to że klasa zapewnia dostęp do jakiegoś zasobu, np.: bazy danych lub pliku.
  Używając singletona możemy kontrolować/ograniczać dostęp do współdzielonego zasobu lub konfiguracji aplikacji.

  Zasada działania wzorca jest dosyć prosta. W momencie kiedy chcesz uzyskać dostęp do obiektu implementującego singleton, odpowiedzialna za niego klasa sprawdza czy nie został już stworzony, jeśli tak - zwróci istniejącą instancje, w innym przypadku utworzy nową. Implementacja takiego zachowania nie jest możliwa z użyciem zwykłego konstruktora ponieważ ten zgodnie z zasadami designu zawsze musi zwrócić nowy obiekt - jak poprawnie zaimplementować singleton opisuje poniżej.

  2. Udostępnia globalny sposób dostępu do tej pojedyńczej instancji.

  Podobnie jak zmienne globalne, wzorzec singleton pozwala Ci uzyskać dostęp do danego obiektu z dowolnego miejsca w aplikacji. Przewagą wzorca nad globalnymi zmiennymi jest ochrona instancji obiektu przed nadpisaniem go innym fragmentem kodu. 

  Kolejną zaletą tego rozwiązania jest to, że nie musisz kopiować kodu który rozwiązuje problem nr 1 do wielu fragmentów aplikacji, a pozostaje on w jednej klasie.


* Ze względu na popularność wzorca, często spotykanym jest nazywanie czegoś Singletonem nawet jeśli rozwiązuje tylko jeden z wymienionych wyżej problemów. 


Jak zaimplementować singleton:
  1. Dodaj do klasy prywatne pole które będzie przechowywać instancje singletona
  2. Zadeklaruj publiczną metodę która będzie zwracać instancje singletona
  3. W tej publicznej metodzie zaimplementuj kod który przy pierwszym wywołaniu utworzy nowy obiekt i zapisze go w prywantmy polu, a przy następnych zwróci istniejącą instancje.
  4. Konstruktor tej klasy powinien być prywatny. W ten sposób dostęp do niego będze miała publiczna metoda odpowiedzialna za zwrócenie singletona, ale nie inne obiekty.
  5. W kodzie klienckim używaj publicznej metody by uzyskać dostęp do instancji singletona.

Zalety i wady:
  + Możesz być pewny że klasa będzie miała tylko pojedyńczą instancje.
  + Zyskujesz globalny sposób na dostęp do tej instancji.
  + Obiekt tej klasy jest inicjalizowany dopiero przy pierwszej próbie uzyskania dostępu.

  - Wzorzec łamie zasade pojedyńczej odpowiedzialności - rozwiązuje dwa problemy.
  - Może maskować zły design, np.: gdy różne części aplikacji wiedzą zbyt dużo o sobie nawzajem.
  - Wymaga dodatkowej uwagi w środowisku wielowątkowym, by nie dopuścić do utworzenia obiektu singleton wiele razy.
  - Testy jednostkowe takiego obiektu mogą być problematyczne. Ze względu na prywatny konstruktor wiele frameworków testowych będzie miało problem z utworzeniem mocku.


Przykładowy kod: https://github.com/rafczow/php-patterns-practice/tree/master/src/Singleton


Powiązane wzorce:
  Facade
  Flyweight