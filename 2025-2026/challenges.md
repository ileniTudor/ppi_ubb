# Teme de proiect MIRPR 2025-2026

Mai jos găsiți lista proiectelor propuse pentru acest an. Dați click pe săgeată sau pe titlu pentru a vedea detaliile.

---

## Project 1
<details>
<summary><strong>Conversational Avatar Production</strong> (Owner: Alexandru Manole)</summary>
<br>

<img src="projects/avatar.webp" width="150" alt="Avatar Project">

### Conversational Avatar Production

#### Scop
Dezvoltarea unui sistem conversațional care răspunde la întrebări textuale în mod vocal prin intermediul unui avatar. 
De exemplu:
- **UBB-bot**: răspunde la întrebări despre UBB și are ca avatar imaginea lui Janos Bolyai.
- **Turing-bot**: răspunde la întrebări despre AI și are ca avatar imaginea lui Alan Turing.

#### Ideea de bază
În lumea digitală, interacțiunea cu avatare animate devine tot mai importantă (asistenți virtuali, jocuri, educație). Crearea animațiilor realiste este costisitoare. Folosind Machine Learning, acest proces poate fi automatizat pentru a reproduce mișcările buzelor și expresiile faciale în timp real, pe baza unui input audio sau text.

#### Bibliografie și Cerințe
- **Generare imagini:** Utilizarea modelelor Stable Diffusion, ex. Flash Diffusion ([paper](https://arxiv.org/pdf/2406.02347), [git](https://github.com/gojasper/flash-diffusion)).
    - Comparare cu alte modele.
    - Antrenare de la 0 pe set de date mic.
    - Fine-tuning folosind LoRA.
    - Antrenare Flash Diffusion pentru ControlNet.
- [Recomandări versiune precedentă](https://github.com/lauradiosan/AI-UBB/blob/main/2024-2025/labs/projects.md)

</details>

---

## Project 2
<details>
<summary><strong>Identificarea defectelor software</strong> (Owner: Laura Cernau)</summary>
<br>

<img src="projects/code.jpg" width="150" alt="Code Quality">

### Identificarea defectelor software

#### Scop
Dezvoltarea unui model AI bazat pe LLM care să identifice defectele software în codul sursă pe baza codului și a metricilor de complexitate. Analizele recente arată că asistenții AI (Copilot) cresc productivitatea dar pot scădea calitatea codului ([Sursa: GitClear](https://www.gitclear.com/coding_on_copilot_data_shows_ais_downward_pressure_on_code_quality)).

#### Ideea de bază
Se va considera o bază de date cu proiecte software. Input-ul pentru LLM poate fi:
- Doar codul sursă al clasei curente.
- Codul sursă al clasei și al claselor părinte.
- Codul sursă + Metricile de complexitate (Complexitate Ciclomatică, Cognitivă, Weighted Methods, Lack of Cohesion, Halstead’s Metrics, Lines of Code).

**Output așteptat:** Defectele software identificate (dacă clasa conține bug-uri și ce tip).

#### Data
- [PROMISE Dataset (Java)](https://www.inf.szte.hu/~ferenc/pdf/FTL18-PROMISE-A%20public%20unified%20bug%20dataset%20for%20Java.pdf)

#### Bibliografie
- [List of research papers on Code LLMs](https://github.com/PurCL/CodeLLMPaper/tree/main)
- Evaluating Source Code Quality with LLMs ([Simões & Venson, 2024](https://www.researchgate.net/publication/383119379_Evaluating_Source_Code_Quality_with_Large_Languagem_Models_a_comparative_study))
- Core: Resolving code quality issues using LLMs ([Wadhwa et al., 2024](https://dl.acm.org/doi/pdf/10.1145/3643762))
- LLMs for Source Code Analysis ([Jelodar et al., 2025](https://www.researchgate.net/publication/390143194_Large_Language_Models_LLMs_for_Source_Code_Analysis_applications_models_and_datasets))
- Do LLMs really do their job? ([Fang et al., 2024](https://www.usenix.org/system/files/sec24fall-prepub-2205-fang.pdf))

</details>

---

## Project 3
<details>
<summary><strong>Helpdesk bazat pe LLM (RAG)</strong> (MateInfo-UBB)</summary>
<br>

<img src="projects/RAG.png" width="150" alt="RAG System">

### Sistem automat pentru helpdesk bazat pe LLM

#### Scop
Dezvoltarea unui sistem inteligent de tip **RAG (Retrieval-Augmented Generation)** care să răspundă la întrebări folosind un LLM și o colecție de documente, specializat pe domeniul informatic/financiar.

#### Ideea de bază
Sistemul va căuta în documente și va genera răspunsuri.
**Se vor compara:**
- Strategii de indexare (TF-IDF, embeddings).
- Modele LLM (pre-trained vs fine-tuned).
- Metode de re-ranking.
- Metode de evaluare (umană vs automată).

#### Data
- [Public RAG Data](https://github.com/MoritzLaurer/rag-demo/tree/master)
- Private data (la cerere).

#### Bibliografie
- **RAG Background:** [LangChain Tutorial](https://python.langchain.com/docs/tutorials/rag/), [RAG Paper (Lewis et al.)](https://arxiv.org/pdf/2005.11401), [RAG from scratch](https://www.freecodecamp.org/news/mastering-rag-from-scratch/).
- **Re-ranking:** [Learning-to-Rank in NLP](https://aclanthology.org/2024.findings-naacl.123.pdf), [LLM-based Rerankers](https://arxiv.org/abs/2508.16757).
- **Evaluation:** [G-Eval (GPT-4)](https://arxiv.org/abs/2303.16634).

</details>

---

## Project 4
<details>
<summary><strong>Identificarea cancerului de plămân</strong> (Owner: Dr. Andrei Roman / Nicolas Musat)</summary>
<br>

<img src="projects/lungCancer.jpeg" width="150" alt="Lung Cancer">

### Identificarea cancerului de plămân

#### Scop
Dezvoltarea unui sistem inteligent ("biopsie virtuală") pentru diagnosticarea timpurie a cancerului pulmonar folosind scanări CT/PET.

#### Ideea de bază
Problema poate fi abordată ca o clasificare multi-label.
Input-ul modelului:
- 3D Segmented CT scans.
- Markeri IHC confirmați prin biopsie.
- Vârstă și gen.

#### Data
- [Kaggle Chest CT-scan images](https://www.kaggle.com/datasets/mohamedhanyyy/chest-ctscan-images/data)
- [LIDC-IDRI Collection](https://www.cancerimagingarchive.net/collection/lidc-idri/)

#### Bibliografie
- Radiogenomic System for Non-Invasive Identification ([Shao et al., 2022](https://doi.org/10.3390/cancers14194823))
- Lung tumor segmentation methods ([Owens et al., 2018](https://doi.org/10.1371/journal.pone.0205003))
- Deep learning for lungs cancer detection ([Javed et al., 2024](https://link.springer.com/article/10.1007/s10462-024-10807-1))

</details>

---

## Project 5
<details>
<summary><strong>Identificarea cancerului de sân</strong> (Owner: Dr. Andrei Roman / Dr. Cristiana Moroz-Dubenco)</summary>
<br>

<img src="projects/breastCancer.jpeg" width="150" alt="Breast Cancer">

### Identificarea cancerului de sân

#### Scop
Utilizarea modelelor Transformer/GNN pentru a identifica tumori maligne și benigne în mamografii, depășind dificultățile interpretării manuale (țesuturi dense, structuri suprapuse).

#### Data
- [MIAS](http://peipa.essex.ac.uk/info/mias.html)
- [DDSM / CBIS-DDSM](https://www.cancerimagingarchive.net/collection/cbis-ddsm/)
- [INbreast](https://www.kaggle.com/datasets/tommyngx/inbreast2012)
- [DBT](https://www.cancerimagingarchive.net/collection/breast-cancer-screening-dbt/)

#### Bibliografie
- **Graph CNNs:** [PyTorch Geometric](https://github.com/pyg-team/pytorch_geometric), [GNN for breast cancer (Chowa et al.)](https://pmc.ncbi.nlm.nih.gov/articles/PMC10725367/).
- **Transformers:** [ViT Paper](https://arxiv.org/pdf/2010.11929), [CrossViT](https://github.com/IBM/CrossViT), [MammoViT (2025)](https://www.mdpi.com/2075-4418/15/3/285).

</details>

---

## Project 6
<details>
<summary><strong>Voice to text - Fișa Pacientului</strong> (Owner: Dr. Alina Baciu)</summary>
<br>

<img src="projects/voice.avif" width="150" alt="Voice to Text">

### Automatizarea întocmirii fișei pacientului

#### Scop
Sistem inteligent care transformă informația audio înregistrată de medic (ex: în timpul unei ecografii) în format text și completează automat rubricile din fișa pacientului.

#### Data
- **Audio:** [Test 1](./projects/voice2text/test1.ogg), [Test 2](./projects/voice2text/test2.ogg) *(Asigurați-vă că fișierele există în folder)*.
- **Model Fișă:** [Patient Template](./projects/voice2text/patient1.odt).

#### Bibliografie
- [Whisper (OpenAI)](https://openai.com/index/whisper/)
- [RobinASR (Romanian)](https://github.com/racai-ai/RobinASR)
- [HuggingFace Speech to Text](https://huggingface.co/docs/transformers/model_doc/speech_to_text)
- [Wav2Vec2 Romanian](https://huggingface.co/gigant/romanian-wav2vec2)

</details>

---

## Project 7
<details>
<summary><strong>Estimarea dificultății cazurilor stomatologice</strong> (Owner: Dr. Mihaela Hedesiu)</summary>
<br>

<img src="projects/endodontie.webp" width="150" alt="Endodontie">

### Identificarea dificultății cazului de endodonție

#### Scop
Estimarea automată a dificultății unui caz de endodonție pe baza radiografiilor periapicale folosind Deep Learning. Sistemul va diferenția între tratamente corecte și incorecte și va sugera dacă cazul necesită trimitere la specialist.

#### Ideea de bază
Tratamentul endodontic are o rată de succes mare, dar erorile (perforații, blocaje) sunt riscante. Evaluarea manuală conform ghidurilor AAE este consumatoare de timp.

</details>

---

## Project 8
<details>
<summary><strong>Causality identification</strong> (Owner: Dr. Dan Blendea)</summary>
<br>

<img src="projects/causality.jpeg" width="150" alt="Causality">

### Identificarea cauzelor insuficienței mitrale

#### Scop
Identificarea cauzelor insuficienței mitrale (MR) plecând de la ecografii cardiace (DICOM). Se va folosi un model **Graph-based CNN** pentru a analiza interdependențele dintre măsurători (volum MR, ventricul stâng, atriu stâng).

#### TODO List
1. Analiza evoluției măsurătorilor în timp (cicluri cardiace).
2. Identificarea interdependențelor.
3. Estimarea cauzelor pe baza grafului.

#### Data
- [Dataset Pacienți (Excel)](./projects/pacienti.xlsx) *(Verificați calea fișierului)*

#### Bibliografie
- [PyTorch Geometric](https://pytorch-geometric.readthedocs.io/en/latest/)
- [CausalGNN](https://arxiv.org/pdf/2312.12477)
- [Neural Granger Causality](https://github.com/harpoonix/GC-xLSTM)

</details>

---

## Project 9
<details>
<summary><strong>Medical dataset generation</strong> (Owner: Mihai Nadas)</summary>
<br>

<img src="projects/medicalData.jpg" width="150" alt="Medical Data">

### Dezvoltarea unui corpus medical în limba română

#### Scop
Crearea unei baze de date medicale (corpus) pentru limba română pentru a susține cercetarea NLP (extragere simptome, codificare ICD-10).

#### Etape
1. Colectare și curățare date reale (anonimizare).
2. Definire scheme (note clinice, conversații).
3. Generare sintetică (Prompt Engineering + LLM).
4. Structurare și etichetare.

#### Bibliografie
- [Romanian NLP Datasets](https://github.com/AndyTheFactory/romanian-nlp-datasets)
- [BioRo Corpus](https://aclanthology.org/anthology-files/pdf/L/L18/L18-1191.pdf)
- [OpenLLM-Ro](https://openllm.ro/)

</details>

---

## Project 10
<details>
<summary><strong>Legal dataset generation</strong> (Owner: Mihai Nadas)</summary>
<br>

<img src="projects/medicalData.jpg" width="150" alt="Legal Data">

### Dezvoltarea unui corpus de documente juridice

#### Scop
Construirea celui mai mare corpus de documente juridice românești (legi, hotărâri, contracte), completat cu date sintetice, pentru antrenarea modelelor de limbaj pe domeniul legal.

#### Resurse
- [Portal Legislativ](https://legislatie.just.ro/)
- [OpenLLM-Ro](https://openllm.ro/)

</details>

---

## Project 11
<details>
<summary><strong>Early Discovery of Anxiety/Depression</strong> (Owner: Cristiana Bogateanu)</summary>
<br>

<img src="images/anxiety.jpeg" width="150" alt="Anxiety">

### Early Discovery of Anxiety/Depression in Teenagers

#### Scop
Identificarea proactivă a semnelor de anxietate și depresie la adolescenți folosind instrumente digitale (chatbots, social media analysis, jocuri video).

#### Bibliografie
- [Phone app uses AI to detect depression](https://home.dartmouth.edu/news/2024/02/phone-app-uses-ai-detect-depression-facial-cues)
- [DeepWell DTx](https://www.deepwelldtx.com/)

</details>

---

## Project 12
<details>
<summary><strong>Digital Triage System</strong> (Owner: Cristiana Bogateanu)</summary>
<br>

<img src="images/triage.jpeg" width="150" alt="Triage">

### Digital Triage System

#### Scop
Un sistem inteligent care ghidează pacienții către cel mai potrivit furnizor medical (specialist, GP, urgențe) pe baza simptomelor, folosind AI conversațional.

#### Bibliografie
- [Infermedica Triage](https://infermedica.com/solutions/triage)
- [Claude AI in Healthcare](https://618media.com/en/blog/claude-ai-in-healthcare-applications/)

</details>

---

## Project 13
<details>
<summary><strong>Real-Time Scene-Aware Assistant (TinyVLM)</strong> (Owner: Mohamed Hassan, Bosch)</summary>
<br>

<img src="images/elderly.jpeg" width="150" alt="Blind Assistance">

### Asistent pentru nevăzători folosind TinyVLM

#### Scop
Dezvoltarea unui asistent vizual care rulează pe dispozitive cu resurse limitate (TinyVLM) pentru a descrie mediul înconjurător persoanelor nevăzătoare în timp real.

#### Data
- [SANPO Dataset](https://research.google/blog/sanpo-a-scene-understanding-accessibility-navigation-pathfinding-obstacle-avoidance-dataset/)
- [Blind people scene descriptions](https://huggingface.co/datasets/mlevytskyi/blind-people-scene-descriptions)

#### Bibliografie
- [TinyVLM Paper](https://openreview.net/pdf?id=lVIkk8p6RN) & [Code](https://github.com/anananan116/TinyVLM)

</details>

---

## Project 14
<details>
<summary><strong>Monitorizarea stării de sănătate (SmartWatch)</strong> (Owner: Zoltan Balint)</summary>
<br>

<img src="images/smartWatch.png" width="150" alt="SmartWatch">

### Analiza datelor de la SmartWatch (Business Intelligence)

#### Scop
Explorarea datelor colectate de ceasuri inteligente (activitate, somn, ritm cardiac) folosind tehnici de Business Intelligence (BI) pentru a oferi insight-uri personalizate de sănătate.

#### Bibliografie
- [Artificial Intelligence Enabled Sleep Health Dashboards](https://ieeexplore.ieee.org/abstract/document/10984363)
- [Digital biomarkers from smartwatch data](https://ieeexplore.ieee.org/abstract/document/9431000)

</details>

---

## Project 15
<details>
<summary><strong>Segmentarea arterei etmoidale anterioare pe CBCT</strong> (Owner: Dr. Filip Iacob)</summary>
<br>

<img src="images/Adenoids_with_endoscopy.webp" width="150" alt="CBCT">

### Segmentarea arterei etmoidale anterioare

#### Scop
Segmentarea automată a Arterei Etmoidale Anterioare (AEA) pe scanări CBCT pentru a reduce riscul de lezare în timpul chirurgiei endoscopice nazale.

#### Bibliografie
- AI algorithm for AEA differentiation ([Huang et al., 2020](https://www.cambridge.org/core/journals/journal-of-laryngology-and-otology/article/an-artificial-intelligence-algorithm-that-differentiates-anterior-ethmoidal-artery-location-on-sinus-computed-tomography-scans/)).

</details>