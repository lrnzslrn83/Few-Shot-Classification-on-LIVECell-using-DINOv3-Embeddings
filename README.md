Questo progetto esplora un approccio di few-shot learning per la classificazione di immagini cellulari utilizzando embedding estratti da DINOv3, un Vision Transformer pre-addestrato in modalità self-supervised.
L’obiettivo è valutare la qualità e la trasferibilità delle rappresentazioni apprese da DINOv3 in uno scenario a bassa disponibilità di dati etichettati, tipico del dominio biomedicale, dove l’annotazione manuale è costosa e limitata.


Le immagini utilizzate provengono dal dataset LIVECell, disponibile pubblicamente su Kaggle:
https://www.kaggle.com/datasets/3eb5e4d9b2d603944dfc1a85fd37c6ba61b2c08ee543bd37342544370a88c71d
LIVECell è un dataset di immagini microscopiche contenente diverse linee cellulari annotate. In questo progetto è stato utilizzato per un task di classificazione few-shot.
Il dataset non è incluso nel repository e deve essere scaricato separatamente tramite Kaggle.

1. Dataset Analysis and Exploration

È stata condotta un’analisi esplorativa del dataset LIVECell per comprendere:
distribuzione delle classi
eventuali squilibri
caratteristiche visive delle diverse linee cellulari
qualità e variabilità delle immagini
Questa fase ha permesso di definire correttamente il setup sperimentale few-shot e di interpretare in modo consapevole le metriche di valutazione.

2. Feature Extraction
Le immagini vengono processate tramite il backbone DINOv3 pre-addestrato, utilizzato esclusivamente come feature extractor congelato. Non viene effettuato fine-tuning del modello, al fine di valutare la qualità intrinseca delle rappresentazioni auto-supervisionate.

3. Few-Shot Experimental Setup
Viene simulato uno scenario k-shot selezionando un numero limitato di esempi per classe. Sono stati testati diversi valori di k per analizzare l’evoluzione delle performance al crescere dei dati supervisionati.

4. Classification in Embedding Space
Gli embedding estratti vengono utilizzati come input per classificatori leggeri, mantenendo separata la valutazione della qualità delle feature dalla complessità del modello finale.

5. Model Selection and Evaluation
Le performance vengono analizzate tramite:
Accuracy globale
Confusion Matrix a conteggi assoluti
Confusion Matrix normalizzata per riga
La configurazione migliore viene identificata sulla base delle metriche aggregate e dell’analisi per classe.

6. Final Retraining
Dopo la selezione della configurazione ottimale, il classificatore viene riaddestrato per consolidare i risultati finali.

Objective
Valutare la robustezza delle rappresentazioni self-supervised di DINOv3 in regime low-data e analizzare la separabilità delle classi nello spazio latente in un contesto biomedicale.
