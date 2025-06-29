on:
- N = nombre total de trigrames en el model
- B = nombre total de trigrames únics

## Classificació de les Frases del Test

Per cada frase:
- Es calculen les probabilitats logarítmiques respecte a cadascun dels models d’idioma.
- S’assigna l’idioma amb la probabilitat més alta.
- Es genera una matriu de confusió per comparar etiquetes reals i predites.

## Resultats i Avaluació

La precisió global (**accuracy**) i la matriu de confusió mostren una alta capacitat del sistema per identificar correctament la major part de les frases. Tanmateix, s’observen errors recurrents especialment en frases curtes i en idiomes amb similitud lèxica elevada, com l’espanyol i l’italià.

### Principals fonts d’error detectades

- **Trigrames comuns entre idiomes**, especialment en llengües romàniques.
- **Frases de poca longitud**, amb menys context per a una classificació precisa.
- **Classificacions insegures**, on la diferència de probabilitat entre el primer i segon idioma era molt petita.

## Propostes de millora

- Incrementar el pes dels trigrames únics o distintius per idioma.
- Ajustar la ponderació dels trigrames comuns.
- Revisar la gestió de frases curtes mitjançant models més sensibles al context.
- Considerar l’ús de models híbrids que combinin trigrames amb altres característiques lingüístiques.

## Llibreries i Eines

- Python
- NLTK
- NumPy
- scikit-learn
- seaborn
- Matplotlib

## Reproducció de l’Experiment

1. Instal·lar les dependències necessàries (`pip install -r requirements.txt`).
2. Col·locar els fitxers de text del corpus a la ruta especificada.
3. Executar els scripts de preprocessament i entrenament.
4. Processar el corpus de test i generar la matriu de confusió.
5. Revisar la precisió i l’anàlisi dels errors.

## Llicència

Aquest projecte s’ha desenvolupat amb finalitats acadèmiques. Per a ús productiu o comercial, es recomana una revisió exhaustiva i una adaptació del model.
