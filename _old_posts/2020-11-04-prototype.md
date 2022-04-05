---
title: "Prototyp"
excerpt_separator: "<!--more-->"
categories:
  - Design patterns
tags:
  - creational design patterns
---

Wzorzec kreacyjny z użyciem którego możesz tworzyć kopie istniejących obiektów bez tworzenia zależności na od ich klas.

<!--more-->

Pierwszym rozwiązaniem które przychodzi na myśl w przypadku tworzenia kopii obiektu jest tradycyjne podejście, utworzenie nowego obiektu tej samej klasy co oryginał, a następnie przekopiowanie wartości wszystkich pól do nowego obiektu. Takie podejście jednak nie sprawdzi się dla wszystkich scenariuszy i ma poważne wady w kontekście czystości kodu. Niektóre pola kopiowanego obiektu mogą być prywatne i nie będzie do nich dostępu w chwili tworzenia kopii. Stosując takie podejście tworzysz w swoim kodzie dodatkową zależność na klasie wspomnianego obiektu. Kolejnym argumentem przeciwko takiemu rozwiązaniu jest to że czasami nie znamy konkretnej klasy która zostanie użyta do implementacji obiektu - znamy tylko jego interfejs. Metody często akceptują każdy przekazany obiekt który implementuje dany interfejs co dodatkowo utrudnia zadanie.

Prototyp adresuje wszystkie te problemy wydzielając kod odpowiedzialny za klonowanie obiektu do pojedyńczej metody tego obiektu. Wzorzec zakłada istnienie wspólnego interfejsu dla wszystkich obiektów które mają wspierać klonowanie. Implementacja takiego interfejsu pozwala na szybkie tworzenie kopii obiektów i uniknięcie wypisanych powyżej wad. Zazwyczaj taki interfejs posiada tylko jedną metode - clone() - która zwraca kopie obiektu. Obiekty które wspierają klonowanie taką metodą nazywamy prototypami.

W kontekście PHP wzorzec Prototype jest dostępny 'out of the box'. Za pomocą słowa kluczowego 'clone' możesz łatwo stworzyć kopie podanego obiektu.
Istotne w tym przypadku jest to, że pola zawierające referencje do zmiennych lub obiektów pozostaną referencjami. W przypadku gdy dostarczona przez język logika kopiowania nie zadziała do końca tak jak tego chcemy, zawsze możemy zdefiniować metodę __clone() w naszym obiekcie i dopisać potrzebne operacje.
Dla szczegółów implementacji warto sprawdzić co mówi na ten temat dokumentacja https://www.php.net/manual/en/language.oop5.cloning.php


Zalety i wady:
  + Klonowanie obiektów bez tworzenia zależności od innych klas
  + Używajac przemyślanych prototypów możesz pozbyć sie powtarzalnego kodu inicjalizujacego obiekty
  + Dobre alternatywa do dziedziczenia gdy masz doczyniena z różnymi konfiguracjami skomplikowanych obiektów
  - Tworzenie kopii bardzo skomplikowanych obiektów z wieloma referencjami wciąż będzie wymagało dodatkowej uwagii

Przykładowy kod: 

Powiązane wzorce:
 Abstract Factory
 Factory Methods
 Memento
