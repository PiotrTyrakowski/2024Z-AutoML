Pipeline pakietu działa w następujący sposób:

1 Pobieranie danych: Na początku pobierane są dane z funduszu Numerai.

2 Trening modeli: Następnie trenowanych jest 31 modeli lightGBM – każdy dedykowany innemu targetowi, który odzwierciedla wydajność akcji w czasie.

3 Optymalizacja cech: Przy użyciu random search dobierane są cechy do liniowej neutralizacji (dla każdego z modeli osobno) w celu maksymalizacji współczynnika Sharpe.

4 Budowa ensemblera: Wyniki z wcześniejszych modeli traktowane są jako nowe cechy (features). Na ich podstawie trenowany jest model typu ensembler, przy czym wykorzystujemy dwa rodzaje – model liniowy oraz lightGBM. W tym etapie przeprowadzany jest dobór hiperparametrów oraz cross-walidacja, aby uzyskać jak najlepszy model.

5 Model Omega: Z wytrenowanych modeli ensemble tworzymy ostateczny model, zwany modelem Omega, który stanowi średnią arytmetyczną wyników poprzednich modeli z kroku czwartego.

6 Weryfikacja i raportowanie: Wyniki modeli są następnie weryfikowane na danych walidacyjnych udostępnionych przez fundusz. Na tej podstawie generowany jest raport w postaci pliku raport.html, prezentującego ich wydajność.

7 Zapisywanie modeli: Wszystkie modele są zapisywane w folderze modele przy użyciu biblioteki pickle.



to activate the environment run:

source add_root_to_path.sh
pip install -r requirements.txt

to run the pipeline run:
python automl_pipeline.py
