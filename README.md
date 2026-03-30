# Wstępne Przetwarzanie Obrazów i Systemy Wizyjne (Computer Vision)

## O projekcie
Repozytorium zawiera zbiór inżynierskich implementacji z zakresu niskopoziomowego przetwarzania obrazów cyfrowych. Skrypty demonstrują zrozumienie fundamentów działania systemów wizyjnych, optymalizacji obliczeń na macierzach oraz przygotowywania danych wizyjnych do dalszej analizy (np. detekcji cech lub segmentacji).

Projekty zostały zrealizowane w architekturze notatników Jupyter, co pozwala na interaktywną wizualizację poszczególnych etapów transformacji obrazu.

## Technologie i Biblioteki
* **Python 3**
* **OpenCV (`cv2`)** – do wczytywania, konwersji i aplikacji filtrów.
* **NumPy** – do bezpośrednich, zoptymalizowanych operacji na macierzach (tensorach) obrazu.
* **Matplotlib** – do tworzenia profili analitycznych, histogramów i wizualizacji map przestrzennych.

## Spis Treści (Notatniki)

### 1. `01_OpenCV_Basics.ipynb` - Przestrzenie Barw i Analiza 3D
* Automatyczne zarządzanie danymi testowymi.
* Konwersja i manipulacja przestrzeniami barw (BGR do RGB, Grayscale).
* Analiza obrazu jako dwuwymiarowej funkcji dyskretnej $L(x,y)$ z wykorzystaniem wizualizacji trójwymiarowej.
* Mapowanie pseudokolorów (Colormaps) w celu poprawy percepcji kontrastu w obrazach jednokanałowych.

### 2. `02_Image_Math.ipynb` - Operacje Punktowe, Arytmetyka i Maskowanie
* Implementacja zoptymalizowanych nieliniowych przekształceń jasności z wykorzystaniem tablic **LUT (Look-Up Table)**.
* Arytmetyka macierzy obrazu (dodawanie, odejmowanie, kombinacja liniowa/blending).
* Obsługa problemów brzegowych sprzętu, takich jak **zjawisko przepełnienia (overflow/saturacja)** typów 8-bitowych (`uint8`) poprzez rzutowanie do przestrzeni 16-bitowej.
* Logika Boole'a stosowana do masek binarnych (AND, OR, XOR, NOT) oraz izolacja regionów zainteresowania (ROI).

### 3. `03_Bit_Slicing.ipynb` - Dekompozycja Bitowa i Kwantyzacja
* Rozbicie 8-bitowego obrazu na niezależne płaszczyzny bitowe (Bit-Plane Slicing) przy użyciu przesunięć bitowych.
* Analiza rozkładu informacji i szumu na najbardziej (MSB) i najmniej (LSB) znaczących bitach.
* Utratna rekonstrukcja obrazu zredukowanego wyłącznie do najstarszych bitów, demonstrująca podstawy mechanizmów kompresji danych wizyjnych.

### 4. `04_Histogram_Equalization_and_Color_Spaces.ipynb` - Analiza Histogramu i Korekcja Kontrastu
* Ekstrakcja i wizualizacja histogramów dla obrazów w skali szarości.
* Liniowe rozciąganie histogramu (Contrast Stretching) maksymalizujące wykorzystanie zakresu dynamiki sensora.
* Nieliniowe, globalne wyrównywanie histogramu (Histogram Equalization) z wykorzystaniem dystrybuanty (CDF).
* Lokalna, adaptacyjna poprawa kontrastu algorytmem **CLAHE** w celu redukcji przesterowań i wzmocnienia szumów.
* Optymalizacja korekcji w obrazach kolorowych poprzez transformację do przestrzeni **HSV** (modulacja wyłącznie kanału luminancji - V, chroniąca przed zaburzeniami barw).

### 5. `05_Image_Binarization_and_Segmentation.ipynb` - Segmentacja i Binaryzacja Adaptacyjna
* Globalna binaryzacja oparta na analizie bimodalności histogramu.
* Implementacja algorytmów automatycznej optymalizacji progu odcięcia: **metoda iteracyjna** oraz optymalna **metoda Otsu** (maksymalizacja wariancji międzyklasowej).
* Kompensacja gradientów oświetlenia (winietowania) za pomocą binaryzacji lokalnej (adaptacyjnej).
* Zaawansowany algorytm **Sauvola-Pietikäinen** wykorzystujący lokalne odchylenie standardowe do wygładzania tła i ostrej detekcji krawędzi.
* Segmentacja przedziałowa (binaryzacja dwuprogowa) z logiką AND do izolacji specyficznych cech (np. koloru skóry).

## Struktura i Zarządzanie Środowiskiem
Projekt został skonfigurowany pod kątem utrzymania czystości repozytorium:
* Skrypty zawierają procedury automatycznego czyszczenia pobranych danych tymczasowych (zdjęć testowych, cache'u algorytmów).
* Plik `.gitignore` zapobiega wyciekowi danych binarnych i folderów środowisk wirtualnych do repozytorium zdalnego.
* Dołączony `.dockerignore` przygotowuje strukturę pod bezproblemową konteneryzację (budowanie obrazów dla aplikacji wizyjnych i systemów wbudowanych).