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

![Adaptive Metrics Overview](https://github.com/dg-creator/Ada-M/blob/main/images/adaptive-metrics-overview.png)
*Rys. 1: Adaptive Metrics Overview*

---

## 2.1 Podstawy teoretyczne

**Obserwowalność (observability)** jest podejściem związanym z monitorowaniem działania aplikacji, które umożliwia zrozumienie stanu systemu na podstawie analizy danych telemetrycznych. Pozwala nie tylko wykrywać problemy, ale również przeprowadzać ich dokładną analizę oraz identyfikować ich przyczyny.

Podstawowymi elementami obserwowalności są:
- *metryki (metrics)* – ilościowe dane opisujące działanie systemu, takie jak liczba żądań, czas odpowiedzi (latency) czy wykorzystanie zasobów,
- *logi (logs)* – szczegółowe komunikaty opisujące zdarzenia zachodzące w systemie, wykorzystywane m.in. w procesie debugowania,
- *ślady (traces)* – informacje umożliwiające śledzenie przepływu żądań pomiędzy mikroserwisami podczas realizacji operacji.

Połączenie tych elementów pozwala na pełniejsze zrozumienie zachowania systemu oraz znacząco przyspiesza proces identyfikacji i rozwiązywania problemów.

![Observability pillars](https://github.com/dg-creator/Ada-M/blob/main/images/observability-pillars.png)
*Rys. 2: Observability pillars*

Przykładem narzędzia wykorzystywanego w ramach obserwowalności jest **Prometheus**, który realizuje model typu *pull*. Jego zadaniem jest cykliczne zbieranie metryk z monitorowanych usług poprzez dedykowane endpointy, najczęściej dostępne pod adresem /metrics. Zebrane dane są następnie przechowywane w bazie szeregów czasowych (TSDB) i mogą być analizowane przy użyciu języka zapytań PromQL. Prometheus integruje się również z systemami wizualizacji, takimi jak Grafana, umożliwiając prezentację danych w formie dashboardów.

**Grafana** jest narzędziem umożliwiającym monitorowanie infrastruktury oraz wizualizację danych telemetrycznych zbieranych z różnych źródeł, takich jak Prometheus, InfluxDB czy PostgreSQL. Pozwala na prezentację metryk w czasie rzeczywistym oraz analizę danych w postaci interaktywnych dashboardów.

Dzięki Grafanie możliwe jest monitorowanie działania systemu, identyfikować problemy oraz analizować kluczowe wskaźniki, takie jak czas odpowiedzi (latency), liczba żądań czy poziom błędów. Narzędzie to wspiera również tworzenie alertów na podstawie zdefiniowanych progów oraz ułatwia interpretację danych dzięki czytelnej wizualizacji.

Jednym z istotnych rozszerzeń platformy Grafana jest funkcjonalność **Adaptive Metrics**, której celem jest optymalizacja liczby przechowywanych metryk. Mechanizm ten analizuje sposób wykorzystania metryk w dashboardach, zapytaniach oraz alertach, a następnie proponuje ich agregację oraz eliminację zbędnych etykiet, co prowadzi do zmniejszenia zużycia zasobów pamięciowych oraz poprawy wydajności zapytań.

W nowoczesnych systemach obserwowalności coraz częściej wykorzystywane są modele językowe (LLM), które wspierają analizę danych telemetrycznych. Umożliwiają one interakcję z systemem przy użyciu języka naturalnego oraz pomagają w interpretacji metryk, identyfikacji problemów i sugerowaniu możliwych rozwiązań.

W kontekście platformy Grafana funkcjonalność ta realizowana jest przez **Grafana Assistant**, który wspomaga użytkowników w procesie diagnostyki oraz analizy danych.

**Model Context Protocol (MCP)** stanowi koncepcyjną warstwę umożliwiającą integrację modeli językowych z zewnętrznymi narzędziami i systemami. Pozwala on na ujednolicenie komunikacji pomiędzy LLM a źródłami danych, takimi jak systemy monitoringu.

![Project scheme](https://github.com/dg-creator/Ada-M/blob/main/images/project-scheme.png)
*Rys. 3: Koncepcyjny schemat architektury projektu (na podstawie materiałów dydaktycznych)*

---

## 2.2 Stos technologiczny

Głównym elementem technologicznym projektu jest środowisko **Kubernetes**, które umożliwia wdrożenie oraz zarządzanie aplikacją mikroserwisową w postaci kontenerów. Dzięki temu możliwe jest odzwierciedlenie rzeczywistych warunków działania systemów rozproszonych oraz generowanie danych telemetrycznych.

Jako aplikacja demonstracyjna wykorzystany zostanie projekt **OpenTelemetry Demo**, który generuje metryki, logi oraz ślady, umożliwiając analizę działania systemu w środowisku obserwowalności.

Do zbierania metryk zastosowany zostanie system **Prometheus**, który w sposób cykliczny pobiera dane z monitorowanych usług. Zebrane dane będą następnie wizualizowane przy użyciu platformy **Grafana Cloud**, która służy do wizualizacji zebranych danych.

W ramach platformy **Grafana** wykorzystana zostanie funkcjonalność **Adaptive Metrics**, służąca do optymalizacji metryk.

Dodatkowo w projekcie uwzględniono wykorzystanie modeli językowych (LLM), które wspomagają proces interpretacji wyników. Komunikacja pomiędzy systemem monitoringu a modelem językowym realizowana jest koncepcyjnie poprzez warstwę **MCP**, pełniącą rolę pośrednika pomiędzy źródłem danych a modelem.

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

