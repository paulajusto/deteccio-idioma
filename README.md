# Identificació Automàtica d'Idiomes Europeus Mitjançant Trigrames

Aquest projecte implementa un sistema de detecció de l’idioma de frases escrites en sis llengües europees: anglès, espanyol, alemany, italià, neerlandès i francès. La classificació es basa en models de llengua construïts amb trigrames de caràcters, combinats amb una tècnica de suavització per evitar el problema de les probabilitats nul·les.

## Objectius

- Processar i netejar corpus multilingües per entrenar models de trigrames.
- Aplicar la tècnica de **suavització de Lidstone** per gestionar trigrames no observats.
- Identificar l’idioma de cada frase d’un conjunt de test, calculant la probabilitat logarítmica segons els models entrenats.
- Generar una matriu de confusió per avaluar el rendiment del sistema i analitzar les causes dels errors de classificació.

## Conjunt de Dades

S’han utilitzat textos en sis idiomes diferents, dividits en corpus d’entrenament i test. Cada frase del test ha estat considerada com la unitat mínima d’identificació.

## Preprocessament

Per garantir la coherència en la creació dels trigrames, s’ha aplicat un preprocessament uniforme als corpus:

1. **Eliminació de dígits** per evitar soroll.
2. **Conversió del text a minúscules** per unificar criteris.
3. **Normalització dels espais en blanc** substituint espais múltiples i tabulacions per un únic espai.
4. **Concatenació de línies** utilitzant dos espais després d’un punt per marcar el final de les frases.

## Creació dels Trigrames

- S’han generat trigrames de caràcters a partir dels corpus d’entrenament.
- S’ha aplicat un **filtrat**, conservant únicament els trigrames amb una freqüència ≥ 5 per centrar-se en els patrons més representatius de cada idioma.

## Model de Llengua i Suavització

Per evitar assignar probabilitats nul·les als trigrames desconeguts en el test, s’ha utilitzat la tècnica de **Lidstone** amb λ = 0,5. Això ha permès atribuir una petita probabilitat a qualsevol trigram absent del conjunt d’entrenament sense penalitzar en excés els trigrames comuns.

La probabilitat de cada trigram es calcula amb la fórmula:

P(trigrama) = (freq(trigrama) + λ) / (N + λ * B)

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
