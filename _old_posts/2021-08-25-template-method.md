---
title: "Template Method"
excerpt_separator: "<!--more-->"
categories:
  - Design patterns
tags:
  - behavioral design patterns
---

Behawioralny wzorzec projektowy który definiuje szkielet algorytmu w superklasie i pozwala subklasom nadpisywać wybrane kroki bez zmiany podstawowej struktury algorytmu.

<!--more-->

Template method sugeruje podział algorytmu na serie wykonywanych kolejno kroków, zapisanie każdego jako osobnej funkcji, a następnie umieszczenie serii wywołań tych funkcji w pojedyńczej metodzie (template method). Kroki mogą być zdefiniowanne jako abstrakcyjne lub dostarczać domyślne implementacje. W celu wykorzystania algorytmu kod kliencki będzie musiał utworzyć nową subklase, zaimplementować abstrakcyjne metody i w razie potrzeby nadpisać opcjonalne (domyślne) metody, ale nie zmieniać metody zawierającej kolejność wywoływania funkcji.


Sposób implementacji:

1. Rozważ czy dany algorytm możesz podzielić na kilka kroków. Zastanów się które z nich będą wspólne dla wszystkich subklas, a które zawsze będą unikatowe.

2. Utwórz klase abstrakcyjną która będzie stanowić podstawe wzorca. Zdefiniuj zbiór abstrakcyjnych metod które będa reprezentować kroki algorytmu. Zadeklaruj metode (template method) która będzie wywoływać różne funkcje realizując kolejne kroki algorytmu. Może być utworzona jako 'final' aby zapobiec nadpisaniu przez subklasy. 

3. Wszystkie metody odpowiedzialne za poszczególne kroki mogą być zdefiniowane jako abstrakcyjne, jednak czasami warto zakodować niektóre z nich wewnątrz superklasy jako domyślna implementacja. Subklasy nie będą musiały implementować ich na nowo.

4. Pomyśl o zastosowaniu dodatkowych hook`ów pomiędzy kluczowymi krokami algorytmu.

5. Dla każdego z wariantów algorytmu stwórz nową subklase. Muszą one implementować wszystkie abstrakcyjne kroki. Opcjonalnie możesz nadpisać również kroki zawierające domyślną implementacje.


Zalety i wady:
+ Open / Closed Principle 
+ Redukcja zduplikowanego kodu poprzez umieszczenie go w superklasie
+ Klasy klienckie mogą nadpisywać wybrane części dużego algorytmu, a jednocześnie są mniej podatne na problemy związane ze zmianami innych jego fragmentów

- Niektóre klasy klienckie mogą być ograniczone przez dostarczony szkielet algorytmu
- Liskov Substitution Principle może zostać złamany poprzez nadpisanie domyślnej implementacji któregoś z kroków w subklasie
- Template method staje się trudniejsze do utrzymania gdy algorytm składa się z wielu kroków


Przykładowy kod: [GitHub][1]


Polecam źródło [Refactoring Guru: Template Method][2] - zawiera długi opis wzorca ze świetnymi przykładami z życia, ilustracjami, diagramami klas i pseudo kodem. Znajdziesz tam również implementacje w różnych językach i opis powiązań z innymi wzorcami.


[1]: https://github.com/rafczow/php-patterns-practice/tree/master/src/TemplateMethod
[2]: https://refactoring.guru/design-patterns/template-method