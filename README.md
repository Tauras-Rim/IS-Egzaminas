# Dujų jutiklių dreifo kompensavimas (Tauras Rimdžius)

Praktinė kolokviumo dalis: UCI Gas Sensor Array Drift duomenų rinkinys (13 910 mėginių, 128 požymiai, 6 dujų klasės, 10 partijų).
Lyginami metodai: kNN (bazinis), SVM be CORAL, CORAL+SVM, SOM ir pagrindinis metodas (CORAL + tiesinis SVM + savimokymas),
bei dvi modifikacijos: signed-log (protokolas A) ir recency-weighting (protokolas B).

## Failai
- `gas_drift_project.ipynb` – visas eksperimentas (duomenų paruošimas, metodai, hipotezės, abliacijos, triukšmo testas, klaidų analizė).
- `figures_*.png` – notebook'o sugeneruoti grafikai.
- `Praktine_DISfm-26_Tauras_Rimdzius.docx` – ataskaita.
- `AI_naudojimo_zurnalas_Tauras_Rimdzius.docx` – AI naudojimo žurnalas.
- Planas – sprendimo įgyvendinimo planas (teorinė kolokviumo dalis).

## Duomenų atsisiuntimas
1. Atsisiųsti: https://archive.ics.uci.edu/dataset/224/gas+sensor+array+drift+dataset
2. Išpakuoti failus `batch1.dat` … `batch10.dat` į aplanką `Dataset/` šalia notebook'o:
```
IS-Egzaminas/
  gas_drift_project.ipynb
  Dataset/batch1.dat ... batch10.dat
```

## Aplinka
Python 3.13.2 (rezultatai gauti su requirements.txt nurodytomis tiksliomis versijomis).
```
pip install -r requirements.txt
```

## Paleidimas (viena komanda)
```
jupyter nbconvert --to notebook --execute gas_drift_project.ipynb --output gas_drift_project_executed.ipynb --ExecutePreprocessor.timeout=-1
```
Trukmė ~45 min 2 branduolių kompiuteryje (skaičiavimai lygiagretinami per `joblib`, `N_JOBS = -1`).
Taip pat galima paleisti visas celes iš eilės Jupyter / VS Code aplinkoje.

## Atkuriamumas
- Fiksuota sėkla `RANDOM_SEED = 42` (duomenų padalijimas, SVC, SOM, triukšmas, mėginių atranka).
- Lygiagretinimas rezultatų nekeičia.
- Galutinės testavimo partijos derinimui nenaudojamos: hiperparametrai parenkami validacijos aibėje
  (protokole A – 70/30 padalijimas 1 partijos viduje, protokole B – paskutinė mokymo partija).
