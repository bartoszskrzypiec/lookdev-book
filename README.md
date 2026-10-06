# Lookdev dla Artystów Technicznych

Książka HTML o lookdevie pod silniki produkcyjne (Arnold, RenderMan), napisana z myślą o
technicznych artystach — nie o programistach piszących shader od zera, tylko o osobach, które chcą
zrozumieć matematykę i rzemiosło stojące za każdym suwakiem: gamma, grade, offset, ASC CDL,
saturacja, IOR, subsurface scattering, aż po ocenę looku pod kalibrowanym oświetleniem.

29 rozdziałów głównych prowadzi od tego, czym w ogóle jest lookdev, przez linear light i przestrzenie
barw, pełną matematykę gradingu, tekstury jako dane wejściowe, budowę shadera produkcyjnego
(aiStandardSurface / PxrSurface), konkretne recepty materiałowe (skóra, metal, szkło, tkaniny,
włosy), oświetlenie i ocenę looku, aż po Część VIII — ten sam warsztat w silnikach czasu
rzeczywistego (Unreal Engine 5, RED Engine, realia gamedevu). Dodatki A–W rozwijają wybrane tematy głębiej niż pozwala na
to rozdział główny — pełne wyprowadzenia macierzy przestrzeni barw, referencje Arnold/RenderMan
parametr po parametrze, kalibracja materiałów według pomiarów. Osobny pomocnik obliczeniowy prowadzi
krok po kroku przez liczenie transformacji kolorystycznych ręcznie.

Trzecia książka w trylogii, siostrzana wobec
[raytracing-book](https://bartoszskrzypiec.github.io/raytracing-book/) (matematyka renderowania) i
[pipeline-book](https://bartoszskrzypiec.github.io/pipeline-book/) (pipeline produkcyjny) — używa
dokładnie tego samego systemu wizualnego i linkuje do obu tam, gdzie temat już ma głębszy wywód
(ACES, OCIO, SSS, displacement, MaterialX/OSL i inne).

**Wersja live:** https://bartoszskrzypiec.github.io/lookdev-book/ — publikacja idzie z gałęzi
`main` przez GitHub Pages (Settings → Pages → Deploy from a branch → `main` / `/(root)`).

## Jak to działa

To są czyste, statyczne pliki HTML z inline'owanym SVG i wspólnym arkuszem stylów w
`assets/style.css`. Zero zależności, zero build stepu, zero npm — otwierasz plik w przeglądarce
(lub całość na GitHub Pages, po skonfigurowaniu) i działa.

```
index.html              — spis treści
matematyka/              — primer "Zanim zaczniesz": potęgi, logarytmy, macierze 3×3
rozdzialy/                — rozdziały główne 1–29 (R.24–28 to część o realtime/gamedevie)
dodatki/                 — dodatki A–W, każdy rozwija konkretny rozdział lub temat
pomocnik/                — pomocnik obliczeniowy: policz transformacje kolorystyczne ręcznie
assets/style.css         — wspólny dark theme dla wszystkich stron (dziedziczony z raytracing-book)
```

Część stron jest **dwujęzyczna (EN/PL)** — przełącznik języka w prawym górnym rogu, wybór zapisuje
się w przeglądarce i trzyma się przy przechodzeniu między stronami. Obie wersje językowe siedzą w
tym samym pliku HTML, więc działa to także bez JavaScriptu. Dziś dwujęzyczne są: Rozdział 14 i cała
Część VIII (R.24–28); reszta książki jest póki co wyłącznie po polsku.

## Status projektu

To jest żywy projekt, nie jednorazowa publikacja — dokładnie jak obie poprzedniczki. Na start
istnieje pełna struktura i spis treści: każdy rozdział i dodatek ma już ustalony tytuł, miejsce w
książce i jednozdaniową zajawkę, ale **treść jest dopiero pisana** — sesja po sesji, rozdział po
rozdziale. Jeśli otwierasz jakąś stronę i widzisz tylko panel „W przygotowaniu", to nie błąd — po
prostu jeszcze do niej nie doszliśmy.
