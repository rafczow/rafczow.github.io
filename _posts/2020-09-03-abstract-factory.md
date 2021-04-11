---
title: "Design patterns: Abstract Factory"
excerpt_separator: "<!--more-->"
categories:
  - Blog
tags:
  - designs pattern
  - creational design patterns
---

Wzorzec kreacyjny pozwalający na tworzenie różnych wariantów wybranego abstrakcyjego obiektu lub obiektów. Obiekty wychodzące od tej samej abstrakcji różnią się na poziomie konkretnych klas ale mogą ze sobą współpracować, realizują podobne zadania i są powiązane na wysokim poziomie koncepcyjnym.

<!--more-->

Abstract factory definiuje interfejs do tworzenia obiektów jednej rodziny pozostawiając szczegóły ich powstawania konkretnej fabryce. Jedna fabryka implementująca ten interfejs odpowiada jednemu wariantowi obiektu.

Aplikacja tworzy obiekt wywołując metode jego fabryki zamiast bezpośredniego użycia konstruktora obiektu. Działania na fabrykach i obiektach odbywają się przez ich abstrakcyjne interfejsy co pozwala aplikacji działać z dowolnym wariantem bez wiedzy o jego konkretnym typie.

Zalety i wady:
  + Open/Closed Principle. Dodawanie kolejnych wariantów nie ingeruje w kod aplikacji wykorzystujacy obiekty pochodzące z fabryki.
  + Single Responsibility Principle. Tworzenie obiektu wydzielone do osobnego miejsca ułatwia utrzymanie kodu.
  + Zapewniona kompatybilność wszystkich obiektów pochodzących z fabryki.
  + Aplikacja nie jest uzależniona od jednego wariantu obiektów.

  - Złożoność kodu wzrasta wraz z ilością nowych wariantów

Sposób implementacji:
1. Zaplanuj siatke typów obiektów i ich możliwych wariantów
2. Zadeklaruj abstrakcyjne interfejsy dla wszystkich typów obiektu. Nastepnie stwórz konkretne obiekty implementujące te interfejsy.
3. Zadeklaruj interfejs Abstract Factory z osobną metodą dla każdego typu, która zwraca jego abstrakcyjny interfejs.
4. Zaimplementuj fabryki (wykorzystując interfejs abstract factory), po jednej dla każdego z wariantów.
5. Dodaj kod inicjalizujący fabryke. Powinien tworzyć instancje jednej z konkretnych fabryk w zależności np. od konfiguracji aplikacji lub środowiska. Przekaż utworzoną fabryke do wszystkich klas tworzących obiekt danego typu.
6* Jeśli refaktoryzujesz: przeszukaj kod w celu odnalezienia wszystkich bezpośrednich utworzeń obiektu przez constructor i zastąp je wywołaniami odpowiedniej metody na fabryce.

Przykładowy kod: https://github.com/rafczow/php-patterns-practice/tree/master/src/Abstract%20Factory

Powiązane wzorce:
  Factory Method
  Builder
  