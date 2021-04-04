---
title: "Design patterns: Factory Method"
excerpt_separator: "<!--more-->"
categories:
  - Blog
tags:
  - design patterns
---

Wzorzec kreacyjny który dostarcza interfejs do tworzenia obiektów w wykorzystującej je klasie, jednocześnie z użyciem dziedziczenia pozwala zmienić konkretny typ obiektu który zostanie stworzony.

<!--more-->

Factory method sugeruje zastąpienie bezpośredniego tworzenia obiektów przez operator new i zamiast nich używanie specjalnej metody jako ich fabryki. Takie rozwiązanie umożliwia nadpisanie metody za pomocą dziedziczenia w celu zmiany zwracanego przez nią typu obiektu. Jedynym ograniczeniem jest to, że podklasy implementujace factory method muszą zwracać obiekty implementujące ten sam interfejs lub pochodzące od tej samej bazowej klasy. Kod aplikacji który używa factory method nie widzi różnicy pomiedzy zwróconymi przez nią obiektami, co pomaga ukryć specyfike ich tworzenia przez logiką biznesową.

Zalety i wady:
 + Brak bezpośredniego powiązania konkretnych obiektów z klasą je wykorzystującą.
 + Single Responsibility Principle. Kod tworzący obiekt jest wydzielony do osobnej klasy.
 + Open/Closed Principle. Nowe warianty obiektu mogą być utworzone bez ingerencji w istniejący kod.
 - Złożoność kodu wzrasta ponieważ wzorzec wymaga stworzenia wielu dodatkowych klas.
 
Sposób implementacji:
1. Stwórz klasy konkretnych obiektów które implementują ten sam interfejs. Intefejs ten powinien definiować metody które znajdą sensowne zastosowanie w każdym z obiektów.
2. Dodaj abstrakcyjną metode fabryki (factory method) w klasie która wykorzystuje obiekty (creator). Zwracany przez metode typ powinien odpowiadać utworzonemu wcześniej interfejsowi. (Metoda nie musi być abstrakcyjna, możesz zaimplementować w niej domyślne zachowanie)
3. Stwórz zbiór podklas implementujących te metode, po jeden dla każdego wariantu obiektu. Umieść w nich kod odpowiedzialny za tworzenie każdego z wariantów.

Przykładowy kod: https://github.com/rafczow/php-patterns-practice/

Powiązane wzorce:
 Abstract Factory
 Builder
 Template Method