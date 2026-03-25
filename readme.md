# Ada-M (Adaptive Metrics)

### Opis zadania
Grafana Adaptive Metrics umożliwia kontrolę rosnącej liczby metryk oraz związanych z nimi kosztów w Grafana Cloud. 

Poprzez analizę sposobu wykorzystania metryk w dashboardach, alertach, regułach zapisu (recording rules) oraz zapytaniach, narzędzie dostarcza rekomendacje dotyczące agregacji rzadko używanych metryk do postaci o niższej kardynalności. 

System na bieżąco ponownie analizuje sposób wykorzystania metryk, aktualizując rekomendacje w zależności od zmieniających się potrzeb w zakresie obserwowalności.

Celem projektu jest zaprezentowanie wykorzystania Grafana Adaptive Metrics na przykładzie aplikacji demonstracyjnej. Aplikacja demo powinna zostać wdrożona w klastrze Kubernetes w celu generowania danych wizualizowanych następnie w Grafana.

## Autorzy
* Gabriela Dumańska
* Diana Hunchak
* Konrad Tendaj
* Stas Kochevenko

---

## 1. Wprowadzenie

Współczesne systemy informatyczne coraz częściej budowane są w oparciu o architekturę mikroserwisową, która pozwala na zwiększenie skalowalności, elastyczności oraz łatwiejsze wdrażanie nowych funkcjonalności. Jednak wraz ze wzrostem liczby usług rośnie złożoność systemu, a zarządzanie komunikacją między serwisami, utrzymanie spójności danych oraz obsługa awarii stają się istotnym wyzwaniem.

Aplikacje działają w środowiskach rozproszonych, w których mogą występować opóźnienia sieciowe, problemy z komunikacją między usługami oraz częściowe awarie. W takich warunkach kluczowe znaczenie ma skuteczne monitorowanie systemu oraz szybkie wykrywanie problemów.

Klasyczne podejścia do monitoringu opierają się głównie na statycznym zbieraniu metryk oraz prostych systemach alertowania wymagających ręcznej konfiguracji progów i reguł. Podejście to sprawdzało się w systemach monolitycznych, jednak w architekturze mikroserwisowej okazuje się niewystarczające.

W odpowiedzi na te ograniczenia rozwinięto koncepcję obserwowalności (observability), opartą na analizie metryk, logów oraz śladów (traces), która umożliwia lepsze zrozumienie zachowania systemu oraz identyfikację anomalii.

Jednym z głównych problemów współczesnych systemów monitorowania jest wysoka kardynalność metryk, czyli duża liczba unikalnych kombinacji etykiet (labels). W praktyce prowadzi to do generowania ogromnej liczby szeregów czasowych, często zawierających szczegółowe, lecz mało użyteczne informacje, takie jak identyfikatory użytkowników, sesji czy pojedynczych żądań.

Etykiety tego typu nie mają istotnego znaczenia dla agregacji danych ani analizy parametrów takich jak opóźnienia (latency) czy liczba błędów, natomiast znacząco zwiększają ilość przechowywanych danych. W efekcie prowadzi to do większego zużycia zasobów, wyższych kosztów oraz pogorszenia wydajności zapytań.

W odpowiedzi na te wyzwania rozwijane są narzędzia takie jak Grafana wraz z funkcjonalnością Adaptive Metrics, które umożliwiają analizę wykorzystania metryk oraz ich optymalizację poprzez agregację i eliminację zbędnych etykiet, przy zachowaniu kluczowych informacji o działaniu systemu.

Dodatkowo zastosowanie modeli językowych (LLM) pozwala na automatyczną analizę danych oraz wspomaganie użytkownika w procesie diagnostyki, umożliwiając bardziej intuicyjną interakcję z systemem.

---

## 2. Podstawy teoretyczne / Stos technologiczny

...

---

## 3. Opis koncepcji case study

...

---

## 4. Architektura wysokopoziomowa

...

---

## 5. Architektura szczegółowa

...

---

## 6. Opis środowiska

...

---

## 7. Metoda instalacji

...

---

## 8. Kroki wdrożenia demo

...

---

### 8.1 Konfiguracja

...

---

### 8.2 Przygotowanie danych

...

---

## 9. Opis demo

...

---

### 9.1 Procedura wykonania

...

---

### 9.2 Prezentacja wyników

...

---

## 10. Podsumowanie

...

---

## 11. Literatura

...

---

