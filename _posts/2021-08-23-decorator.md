---
title: "Decorator"
excerpt_separator: "<!--more-->"
categories:
  - Design patterns
tags:
  - structural design patterns
---

Strukturalny wzorzec projektowy który pozwala rozbudować obiekt o nowe zachowania poprzez umieszczenie go wewnątrz specjalnych obiektów zawierających definicje tych zachowań.

<!--more-->

Alternatywna nazwa tego wzorca to "Wrapper", idealnie oddaje ona pomysł który reprezentuje. W tym przypadku Wrapper to obiekt który posiada referencje do innego obiektu, zawiera ten sam zbiór metod jak połączony obiekt i deleguje do niego wszystkie żadania które otrzymuje. Jego zaletą jest możliwość wykonania dodatkowej pracy przed lub po wywołaniu metody orginalnego obiektu. 

Z wykorzystaniem wspólnego interfejsu dla wrappera oraz bazowego obiektu tworzymy prawdziwy Dekorator. Z perspektywy aplikacji obiekty te będą identyczne. Istotną koncepcją jest użycie wspomnianego interfejsu również jako typu dla pola z referencją, dzięki temu będziemy mogli opakować nie tylko bazowy obiekt ale też dokładać kolejne "opakowania". Z każdym kolejnym nałożonym na obiekt dekoratorem dokładamy nowe zachowania które zostaną wykonane oprócz orginalnego kodu.

Kod aplikacji jest odpowiedzialny za dobór odpowiednich dekoratorów do wykonywanego aktualnie zadania. Faktycznym obiektem na którym klient wywołuje żądania będzie ostatni dodany dekorator, ale ze względu na wspólny interfejs nie będzie to miało znaczenia czy pracuje z "czystym" komponentem czy udekorowanym. 

Dekorator i Proxy strukturalnie wyglądają podobnie ale ich założenia różnią się diametralnie. Oba wzorce wykorzystują kompozycje w której jeden obiekt wykorzystuje drugi do wykonania jakieś pracy. Jednak Proxy zazwyczaj samo zarządza cyklem życia powiązanego obiektu, podczas gdy kompozycja Dekoratorów jest zawsze kontrolowana przez kod kliencki. W przypadku Proxy klient nie jest świadomy jego istnienia, natomiast aby poprawnie wykorzystać Dekoratory musi znać ich odpowiedzialności.


Sposób implementacji:

1. Zweryfikuj czy bazowa klasa implementująca kilka zachowań może zostać podzielona na bazowy komponent z kilkoma dodatkowymi warstwami.
2. Stwórz interfejs komponentu z zadeklarowanymi metodami które będą wspólne dla wszystkich warstw.
3. Zaimplementuj bazowy komponent który realizuje swoją podstawową odpowiedzialność.
4. Stwórz klase bazowego dekoratora. Powinna zawierać pole które będzie referencją do przekazanago komponentu. 
Typ wspomnianego pola powinien wskazywać na interfejs komponentu, a nie konkretną implementacje - w ten sposób możliwe będzie przechowywanie w niej zarówno bazowego komponentu albo dekoratorów. Bazowy dekorator musi delegować całą pracę do opakowanego komponentu.
5. Upewnij się, że wszystkie klasy implementują interfejs komponentu.
6. Stwórz klasy dekoratorów poprzez dziedziczenie z bazowego dekoratora. Każdy konkretny dekorator musi wykonywać swoją odpowiedzialność przed lub po odwołaniu do metody rodzica (który zawsze odwoła się do opakowanego komponentu).
7. Kod kliencki musi być odpowiedzialny za tworzenie dekoratorów i komponowanie ich według potrzeby.


Zalety i wady:

+ Single Responsibility Principle - zamiast jednej dużej klasy z różnymi odpowiedzialnościami implementujemy możliwe zachowania w mniejszych klasach
+ Rozszerzanie możliwości obiektu bez tworzenia klas dziedziczących
+ Stosując wiele dekoratorów dla jednego obiektu możemy przypisać mu kilka dodatkowych zachowań
+ Możemy dodawać/usuwać odpowiedzialności z obiektu w trakcie wykonywania kodu

- Usunięcie konkretnego dekoratora z większego stacku jest trudne
- Ciężko zaimplementować dekorator w taki sposób, aby kolejność jego wykonywania nie miała znaczenia
- Wstępna konfiguracja kolejnych warstw dekoracji w kodzie kliencki będzie wyglądać mało elegancko


Przykładowy kod: [GitHub][1]


Na podstawie:
[Refactoring Guru: Decorator][2]


[1]:https://github.com/rafczow/php-patterns-practice/tree/master/src/Decorator
[2]:https://refactoring.guru/design-patterns/decorator