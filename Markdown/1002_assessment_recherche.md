---
jupytext:
  formats: md:myst
  text_representation:
    extension: .md
    format_name: myst
kernelspec:
  display_name: Python 3
  language: python
  name: python3
---

# 🏆Selbsttest: Wissen und Praxis

````{admonition} Hinweis
:class: hinweis
Diese Übungsaufgaben dienen Ihrer Selbsteinschätzung und helfen Ihnen, das im Kapitel Gelernte zu reflektieren.

Sie können die Fragen in beliebiger Reihenfolge bearbeiten und die Beantwortung auch mehrfach versuchen. 

**So funktioniert es:**
- Wählen Sie bei jeder Frage die Antwort(en) aus, die Sie für richtig halten
- Lesen Sie das Feedback zu den einzelnen Antwortoptionen sorgfältig durch
- Die Erklärungen helfen Ihnen, Ihr Verständnis zu vertiefen – auch bei korrekten Antworten 

Es erfolgt keine Bewertung oder Speicherung Ihrer Ergebnisse. Nutzen Sie dieses Assessment, um Wissenslücken zu identifizieren und gegebenenfalls die entsprechenden Abschnitte des Kapitels nochmals zu bearbeiten. 

**Geschätzte Zeit**: XX

Viel Erfolg!
````

### Aufgabe 0: Test html

```{} 
<style>
/* ---------- layout wrapper ----------------------------------------- */
.dnd-exercise{                     /* NEW */
  display:flex; flex-direction:column;
  align-items:flex-start;          /* left-align each row */
  gap:1.2rem;                      /* space between the three rows */
}

/* ---------- chips --------------------------------------------------- */
.dnd-item{
  background:#eef2ff; border:1px solid #4f46e5;
  border-radius:.5rem; padding:.35rem .75rem; margin:.25rem;
  font-weight:500; box-shadow:0 1px 2px rgba(0,0,0,.06);
  cursor:move; transition:transform .15s, box-shadow .15s;
}
.dnd-item:active{transform:scale(.95);box-shadow:0 4px 6px rgba(0,0,0,.15)}

/* ---------- containers (choices & target) --------------------------- */
.dnd-box{
  min-height:3rem; min-width:8rem;
  padding:.5rem .6rem; margin:0;
  border:2px dashed #9ca3af; border-radius:.75rem;
  display:flex; flex-wrap:wrap; gap:.4rem; align-items:center;
  transition:border-color .2s, background .2s;
}
.dnd-box.dragover{background:#fefce8;border-color:#4f46e5}
.dnd-box.ok{background:#f0fdf4;border-color:#16a34a}

/* ---------- buttons ------------------------------------------------- */
.dnd-btn{
  background:#4f46e5;color:#fff;
  border:0;border-radius:.5rem;
  padding:.45rem 1.1rem;margin-right:.6rem;
  font-weight:500;cursor:pointer;transition:background .2s;
}
.dnd-btn:hover{background:#4338ca}
</style>

<!-- ░░░   EXERCISE   ░░░ -->
<div class="dnd-exercise">             <!--  🚀  NEW wrapper  -->

  <!-- Row 1 – choices -->
  <div id="choices" class="dnd-box">
    <span class="dnd-item" draggable="true" data-key="2">2</span>
    <span class="dnd-item" draggable="true" data-key="9">9</span>
    <span class="dnd-item" draggable="true" data-key="4">4</span>
    <span class="dnd-item" draggable="true" data-key="5">5</span>
  </div>

  <!-- Row 2 – target -->
  <div id="target" class="dnd-box" data-answer="2,5"></div>

  <!-- Row 3 – buttons -->
  <div>
    <button class="dnd-btn" onclick="checkDND()">Check me</button>
    <button class="dnd-btn" onclick="resetDND()">Reset</button>
  </div>

</div> <!-- /dnd-exercise -->

<script>
let dragElem=null;

/* make every chip draggable */
document.querySelectorAll('.dnd-item').forEach(el=>
  el.addEventListener('dragstart',   e=>dragElem=el)
);

/* helper to add “dragover” highlight */
function makeDroppable(box){
  box.addEventListener('dragover',e=>{
      e.preventDefault(); box.classList.add('dragover');
  });
  box.addEventListener('dragleave',e=>{
      box.classList.remove('dragover');
  });
  box.addEventListener('drop',e=>{
      e.preventDefault(); box.classList.remove('dragover');
      box.appendChild(dragElem);
  });
}
['choices','target'].forEach(id=>makeDroppable(document.getElementById(id)));

function checkDND(){
  const picked=[...document.querySelectorAll('#target .dnd-item')]
               .map(x=>x.dataset.key).sort().join();
  const good  =document.getElementById('target')
               .dataset.answer.split(',').sort().join();
  const tgt=document.getElementById('target');
  if(picked===good){ alert('✅ Correct!'); tgt.classList.add('ok'); }
  else             { alert('❌ Try again'); tgt.classList.remove('ok'); }
}
function resetDND(){
  document.getElementById('target').querySelectorAll('.dnd-item')
          .forEach(el=>document.getElementById('choices').appendChild(el));
  document.getElementById('target').classList.remove('ok');
}
</script>
```

### Aufgabe 0.1 Ranking test

```{raw} html
<!-- ░░░  STYLE & LAYOUT  ░░░  (unchanged – keep the colours you liked) -->
<style>
.dnd-exercise{display:flex;flex-direction:column;align-items:flex-start;gap:1.2rem}
.dnd-item{background:#eef2ff;border:1px solid #4f46e5;border-radius:.5rem;
          padding:.35rem .75rem;margin:.25rem;font-weight:500;cursor:move;
          box-shadow:0 1px 2px rgba(0,0,0,.06);transition:transform .15s,box-shadow .15s}
.dnd-item:active{transform:scale(.95);box-shadow:0 4px 6px rgba(0,0,0,.15)}
.dnd-box{min-height:3rem;min-width:8rem;padding:.5rem .6rem;border:2px dashed #9ca3af;
         border-radius:.75rem;display:flex;flex-wrap:wrap;gap:.4rem;align-items:center;
         transition:border-color .2s,background .2s}
.dnd-box.dragover{background:#fefce8;border-color:#4f46e5}
.dnd-box.ok{background:#f0fdf4;border-color:#16a34a}
.dnd-btn{background:#4f46e5;color:#fff;border:0;border-radius:.5rem;
         padding:.45rem 1.1rem;margin-right:.6rem;font-weight:500;cursor:pointer;
         transition:background .2s}
.dnd-btn:hover{background:#4338ca}
</style>

<!-- ░░░  EXERCISE  ░░░ -->
<div class="dnd-exercise">

  <!-- Row 1 – choices (unordered on purpose) -->
  <div id="choices" class="dnd-box">
    <span class="dnd-item" draggable="true" data-key="2">2</span>
    <span class="dnd-item" draggable="true" data-key="9">9</span>
    <span class="dnd-item" draggable="true" data-key="4">4</span>
    <span class="dnd-item" draggable="true" data-key="3">3</span>
  </div>

  <!-- Row 2 – target;  data-answer is the exact sequence required -->
  <div id="target" class="dnd-box" data-answer="2,4,3,9"></div>

  <!-- Row 3 – buttons -->
  <div>
    <button class="dnd-btn" onclick="checkDND()">Check me</button>
    <button class="dnd-btn" onclick="resetDND()">Reset</button>
  </div>

</div> <!-- /dnd-exercise -->

<script>
let dragElem=null;

/* make every chip draggable */
document.querySelectorAll('.dnd-item').forEach(el=>
  el.addEventListener('dragstart',e=>dragElem=el)
);

/* allow drops on both containers + hover highlight */
function makeDroppable(box){
  box.addEventListener('dragover',e=>{e.preventDefault();box.classList.add('dragover')});
  box.addEventListener('dragleave',e=>box.classList.remove('dragover'));
  box.addEventListener('drop',e=>{
      e.preventDefault();box.classList.remove('dragover');
      box.appendChild(dragElem);
  });
}
['choices','target'].forEach(id=>makeDroppable(document.getElementById(id)));

/* ---------- grading – ORDER MATTERS now ---------------------------- */
function checkDND(){
  const picked=[...document.querySelectorAll('#target .dnd-item')]
               .map(x=>x.dataset.key).join();          // no sort!
  const good=document.getElementById('target').dataset.answer;
  const tgt=document.getElementById('target');
  if(picked===good){
      alert('✅ Correct order!');
      tgt.classList.add('ok');
  }else{
      alert('❌ Not quite – check the sequence.');
      tgt.classList.remove('ok');
  }
}

/* ---------- reset --------------------------------------------------- */
function resetDND(){
  document.getElementById('target').querySelectorAll('.dnd-item')
          .forEach(el=>document.getElementById('choices').appendChild(el));
  document.getElementById('target').classList.remove('ok');
}
</script>
```

### Aufgabe 0.2 Test Python ipywidgets

```{code-cell} ipython3
import ipywidgets as W
from IPython.display import display

wanted = ['2', '4', '3', '9']             # target order

tags = W.TagsInput(
    value=['2', '3', '4', '9'],           # start scrambled
    allowed_tags=['2','3','4','9'],        # limit to valid choices
    allow_duplicates=False,
    tag_style='info',                     # a bit of colour
    layout=W.Layout(width='320px')
)

check  = W.Button(description='Check')
out    = W.Output()

def validate(_):
    with out:
        out.clear_output()
        print('Your order:', tags.value)
        print('✅ Correct!') if list(tags.value)==wanted else print('❌ Try again')

check.on_click(validate)
display(tags, check, out)
```

### Aufgabe 1

**Szenario:** Sie möchten eine eigene Fallstudie zu studentischen Animationsfilmen der 1990er Jahre durchführen. Beschreiben Sie systematisch Ihr Vorgehen bei der Materialrecherche im OPAC der Filmuniversität.

Ihre Antwort sollte folgende Schritte umfassen:  
1. Datenbankauswahl 
2. Zeitraumeingrenzung
3. Gattungsfilterung
4. Erste Ergebnisbewertung 
5. Verfeinerte Suchstrategien

#```{code-cell} ipython3
```{} 
:tags: [remove-input]
import sys
sys.path.append("../quadriga")
from assessment import create_answer_box

create_answer_box('Assessment-1')
```

````{admonition} Musterlösung
:class: solution, dropdown

**1. Datenbankauswahl:**
- Auswahl „Erweiterte Suche" auf der OPAC-Startseite
- Auswahl "Archivkatalog" im Dropdown-Menü „Datenbank"

**2. Zeitraumeingrenzung:**
- Eingabe "1990->1999" im Jahr-Feld
- Beachtung der korrekten Pfeil-Syntax

**3. Gattungsfilterung:**
- Suche nach "Animationsfilm" im Schlagwort-Feld
- Berücksichtigung der Bibliothekssystematik: "Animationsfilm/F"

**4. Erste Ergebnisbewertung:**
- Interpretation der Trefferanzahl
- Mehrfachkatalogisierung reflektieren (Anzahl der Such-Treffer muss nicht der Anzahl der vorhandenen Titel entsprechen)
- Einschätzung der Materialmenge für die Fragestellung: sind genug Titel im Archiv vorhanden

**5. Verfeinerte Suchstrategien:**
- Nutzung weiterer Suchfelder (Stichworte, Titel)
- Kombination verschiedener Suchparameter
````

### Aufgabe 2

# ```{code-cell} ipython3
```{} 
:tags: [remove-input]
from jupyterquiz import display_quiz
import sys
sys.path.append("..")
from quadriga import colors

multiple_choice1 = [{
    "question": """Welche Aussagen zur OPAC-Recherche sind korrekt? (Mehrere Antworten möglich)""",
    "type": "multiple_choice",
    "answers": [
        {
            "answer": "Die Trefferanzahl entspricht immer der exakten Anzahl vorhandener Filme",
            "correct": False,
            "feedback": """× Falsch: Die Trefferanzahl umfasst bibliographische Einträge, nicht unbedingt einzelne Filme. Mehrfachkatalogisierung ist möglich."""
        },
        {
            "answer": "Schlagworte folgen einem kontrollierten Vokabular der Bibliothek",
            "correct": True,
            "feedback": """✓ Richtig: Schlagworte wie "Dokumentarfilm/B" folgen der festgelegten Systematik der Bibliothek."""
        },
        {
            "answer": "Zeiträume werden mit einfachen Bindestrichen \"-\" eingegeben",
            "correct": False,
            "feedback": """× Falsch: Zeiträume werden mit Pfeil-Syntax eingegeben: "1985->1999"."""
        },
        {
            "answer": "Stichworte werden frei vergeben und folgen keiner vorgegebenen Liste",
            "correct": True,
            "feedback": """✓ Richtig: Im Unterschied zu Schlagworten werden Stichworte frei vergeben."""
        },
        {
            "answer": "Einzelne Filme können mehrfach katalogisiert sein",
            "correct": True,
            "feedback": """✓ Richtig: Filme können als Teil von Kompilationen oder auf verschiedenen Datenträgern mehrfach verzeichnet sein."""
        },
        {
            "answer": "Die Vollanzeige enthält nur technische Informationen",
            "correct": False,
            "feedback": """× Falsch: Die Vollanzeige enthält umfassende Informationen: Personen, Gewerke, Projektart, Inhaltsangabe etc."""
        }
    ]
}]

display_quiz(multiple_choice1, colors=colors.jupyterquiz)
```

### Aufgabe 3

Analysieren Sie anhand des Beispiels von Lotte Reiniger (Dang/Junginger, 2024) die Problematik der vermeintlichen "Neutralität" von Metadaten. Gehen Sie dabei auf folgende Aspekte ein:

1. Subjektivität in der Datenerfassung
2. Rolle kontrollierter Vokabulare
3. Historische Kontextualisierung

# ```{code-cell} ipython3
```{} 
:tags: [remove-input]
import sys
sys.path.append("../quadriga")
from assessment import create_answer_box

create_answer_box('Assessment_C-3')
```

````{admonition} Musterlösung
:class: solution, dropdown

**1. Subjektivität in der Datenerfassung:**
- Verständnis, dass Metadaten Wertvorstellungen widerspiegeln 
- Beispiel: Unterschiedliche Berufsbezeichnungen für dieselbe Person
- Auswirkungen auf sozialen Status und Wahrnehmung

**2. Rolle kontrollierter Vokabulare:**
- Einfluss vorgegebener Begriffslisten auf Beschreibungen
- Ausschluss bestimmter Bezeichnungen durch Systemvorgaben
- Unterschiede zwischen strukturierten Feldern und Freitexten

**3. Historische Kontextualisierung:**
- Metadaten als historische Quellen verstehen
- Erfassung dessen, was zu bestimmten Zeiten als relevant galt
- Notwendigkeit der Kontextualisierung und Reflexion der Entstehungsbedingungen
````

### Aufgabe 4

A. Erstellung von Visualisierungen zur zeitlichen Verteilung  
B. Suche nach Stichworten "Grenze", "Mauer", "Grenzübertritt"  
C. Sichtung ausgewählter Filme zur Vertiefung  
D. Definition der Suchbegriffe und Synonyme  
E. Eingrenzung des Grundkorpus (1985-1999)  
F. Export der Metadaten  

# ```{code-cell} ipython3
```{} 
:tags: [remove-input]
from jupyterquiz import display_quiz
import sys
sys.path.append("..")
from quadriga import colors

multiple_choice2 = [{
    "question": """Welche Schritte sind für die Bildung eines thematischen Teilkorpus zum Thema "Grenze" notwendig? Bringen Sie die Schritte in die richtige Reihenfolge:""",
    "type": "multiple_choice",
    "answers": [
        {
            "answer": "E → D → B → F → A → C",
            "correct": True,
            "feedback": """✓ Richtig! Die korrekte Reihenfolge ist:
1. E - Grundkorpus definieren: Zeitliche und institutionelle Eingrenzung
2. D - Suchbegriffe definieren: Systematische Begriffsfindung zum Themenfeld
3. B - Suchvorgang: Anwendung der Suchstrategie
4. F - Datenexport: Strukturierte Datensammlung für die weitere Verarbeitung
5. A - Visualisierung: Erste quantitative Analyse
6. C - Qualitative Validierung: Vertiefung und Konkretisierung der Ergebnisse"""
        },
        {
            "answer": "D → E → B → A → F → C",
            "correct": False,
            "feedback": """× Falsch: Der Grundkorpus sollte vor der Definition der Suchbegriffe eingegrenzt werden, um den thematischen Rahmen zu bestimmen."""
        },
        {
            "answer": "E → B → D → F → A → C",
            "correct": False,
            "feedback": """× Falsch: Die Definition der Suchbegriffe sollte vor der eigentlichen Suche erfolgen, um eine systematische Strategie zu entwickeln."""
        },
        {
            "answer": "B → D → E → F → A → C",
            "correct": False,
            "feedback": """× Falsch: Ohne vorherige Eingrenzung des Grundkorpus und Definition der Suchbegriffe wäre die Suche unsystematisch."""
        }
    ]
}]

display_quiz(multiple_choice2, colors=colors.jupyterquiz)
```

### Aufgabe 5

Vergleichen Sie die Herangehensweise dieser Fallstudie („Studentische Filme der Filmuniversität zur Wendezeit") mit einer hypothetischen Studie zu "Studentischen Filmen während der COVID-19-Pandemie (2020-2022)". Analysieren Sie:

1. Ähnlichkeiten in der Methodik
2. Unterschiede in den Herausforderungen
3. Anpassungen der Forschungsfragen

# ```{code-cell} ipython3
```{} 
:tags: [remove-input]
import sys
sys.path.append("../quadriga")
from assessment import create_answer_box

create_answer_box('Assessment_C-5')
```

````{admonition} Musterlösung
:class: solution, dropdown

**1. Ähnlichkeiten in der Methodik:**
- Grundlegende Schritte der Materialrecherche 
- Bedeutung von Metadaten und deren kritische Reflexion
- Notwendigkeit der Operationalisierung
- Kombination quantitativer und qualitativer Ansätze

**2. Unterschiede in den Herausforderungen:**
- Verfügbarkeit digitaler vs. analoger Materialien
- Unterschiedliche rechtliche Rahmenbedingungen
- Temporale Nähe vs. historische Distanz
- Veränderte Lehrpläne und Produktionsbedingungen

**3. Anpassungen der Forschungsfragen:**
- Spezifische historische Kontexte (gesellschaftliche Umbrüche vs. Pandemie)
- Unterschiedliche thematische Schwerpunkte
````


