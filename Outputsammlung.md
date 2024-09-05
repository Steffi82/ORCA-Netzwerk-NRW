<!--
author:   Your Name

email:    your@mail.org

icon:     img/icon.png

version:  0.0.1

language: de

narrator: US English Female

comment:  Material-Finder basierend auf dem Fischbestimmer.

link:     style.css

script:   https://cdnjs.cloudflare.com/ajax/libs/PapaParse/5.3.1/papaparse.min.js

@onload

const baseURL = (new URL("img", window.location.search.substr(1))).href

window["material"] = {
  "level.beginner": null,          
  "level.praktiker": null,         
  "level.experte": null,           

  "praxiskategorie.oer_finden": null,       
  "praxiskategorie.oer_herstellen": null,   
  "praxiskategorie.oer_lernen": null,       
  "praxiskategorie.oer_lehren": null,       
  "praxiskategorie.oer_einfuehren": null,   
  "praxiskategorie.oer_managen": null,      
  "praxiskategorie.oer_forschen": null,     

  "media.audio": null,
  "media.video": null,
  "media.textdoc": null,
  "media.selbstlernen": null,
  "media.webseite": null,
  "media.h5p": null,
  "media.presentation": null,
}

window["button"] = function(title, active, image) {
  const color = active ? '#f0842c' : "black";  
  return `<div style="padding: 8px; color: ${color}">
    <h4>${title}</h4>
    <img src="${image}" loading="lazy">
  </div>`;
}

window.material_filter = function() {
  if (window.material) {
    let items = []
    for (const [item, selected] of Object.entries(window.material)) {
      if (selected) {
        items.push(item)
      }
    }

    let result = []

    for (const material of window.material_db) {      
      let rslt = true

      for (const item of items) {
        if (!material[item]) {  
          rslt = false
          break
        }
      }

      if (rslt) {
        result.push(material.name)
      }
    }

    const div = document.getElementById("results")

    if (div) {
      let list = "<br><h3>Gefundene Materialien</h3>"

      for(const material of result) {
        let url = material.toLocaleLowerCase().replace(/ /g, "-")
        list += `<a style="display: inline-flex; padding: 1rem; margin: 1rem; border: 1px solid black" href="#${url}"><span><h4>${material}</h4><img src="${baseURL}/${url}/thumbnail.png"></span></a>`
      }

      div.innerHTML = list
    }
  }
}

const CSV=`name,level.beginner,level.praktiker,level.experte,praxiskategorie.oer_finden,praxiskategorie.oer_herstellen,praxiskategorie.oer_lernen,praxiskategorie.oer_lehren,praxiskategorie.oer_einfuehren,praxiskategorie.oer_managen,praxiskategorie.oer_forschen,media.audio,media.video,media.textdoc,media.selbstlernen,media.webseite,media.h5p,media.presentation
OER Policy‐Karte und Karte der Netzwerkstellen in NRW,true,false,false,false,false,false,false,false,true,false,false,false,false,false,false,true,false,false
infOERmiert ‐ Der OER‐Blog vom Netzwerk Landesportal ORCA.nrw.,true,false,false,true,true,true,true,true,true,true,true,false,false,false,false,true,false,false`

Papa.parse(CSV, {
  quotes: false,
  header: true,
  dynamicTyping: true,
  complete: function(data){
    window.material_db = data.data;
    setTimeout(window.material_filter, 2000);
  }
})

@end

@button
<script input="button" run-once="true" modify="false">
  function show () {
    if (window.material && window.button) {
      if(window.material["@0"] == null) {
        window.material["@0"] = false
      } else {
        window.material["@0"] = !window.material["@0"]
        window.material_filter()
      }
      send.html(window.button("@1", window.material["@0"], "@2"))

    } else {
      setTimeout(function() {
        show()
      }, 100);  
    }  
  }

  show()
</script>
@end

# Material-Finder


# Output Netzwerk ORCA.

Willkommen, das ist ein Test um zu schauen ob der Fischfinder funktioniert

![](Bilder/Header.png)        


*das ist erstmal ein Platzhalter. Ich würde  den wie unten auf 1200px verbreitern, wenn die Darstellung konstistent gut ist, die Medientypen in der Farbigkeit der Hintergründe weiter unten spezifisch aufgreifen und eine kleine Hommage an OER und Oder ORCA einbauen. Wobei, letzters könnte ja ins Impressum durch einen "gefördert von" Abbinder.*

Für Inspiration einfach entlang der Seitenleiste durchklicken.


<!-- Hinweis: die Nummern in den Hinweisen beziehen sich auf die Zeilennummern in der Output-Excel-Liste. -->

---

<!--
persistent: true
-->

<details>

<summary> Level </summary>

__Level__

@[button(level.beginner,Einsteiger)](Bilder/L-Einsteiger.png)
@[button(level.praktiker,Praktiker)](Bilder/L-Praktiker.png
@[button(level.experte,Experte)](Bilder/L-Experte.png)

</details>

---

details>

<summary> Praxiskategorie </summary>

__Praxiskategorie__

@[button(praxiskategorie.oer_finden,OER finden)](Bilder/B-1.png)
@[button(praxiskategorie.oer_herstellen,OER herstellen)](Bilder/B-2.png)
@[button(praxiskategorie.oer_lernen,Mit OER lernen)](Bilder/B-3.png)
@[button(praxiskategorie.oer_lehren,Mit OER lehren)](Bilder/B-4.png)
@[button(praxiskategorie.oer_einfuehren,OER einführen)](Bilder/B-5.png)
@[button(praxiskategorie.oer_managen,OER managen)](Bilder/B-6.png)
@[button(praxiskategorie.oer_forschen,Über OER forschen)](Bilder/B-7.png)

</details>

---

<details>

__Medienart__

@[button(media.audio,Audio)](Bilder/M-1.png)
@[button(media.video,Video)](Bilder/M-2.png)
@[button(media.textdoc,Textdokument)](Bilder/M-3.png)
@[button(media.selbstlernen,Selbstlernkurs)](Bilder/M-4.png)
@[button(media.webseite,Webseite)](Bilder/M-5.png)
@[button(media.H5P,Webseite)](Bilder/M-5.png)
@[button(media.presentation,Praesentation)](Bilder/M-5.png)

</details>

---

<!-- 01 -->
## OER Policy‐Karte und Karte der Netzwerkstellen in NRW  
`Webseite`
Die Karte zeigt **Hochschulstandorte** der DH.nrw und kennzeichnet solche, die eine **OER Policy veröffentlicht** haben.
![](MaterialienIntros/Webseite_Karte-OER-Policy‐Netzwerkstellen-NRW_CCBY40.jpg)
***`Medienformat:`*** *HTML* ***`erstellt/bearbeitbar mit:`*** *Web-Editor* <br>
***`Niveaustufe(n):`*** Einsteiger (Starter) <br>
***`Praxiskategorie(n)`*** *OER managen* <br>
***`Metadaten:`*** *Karte; HTML; Farbschema; OER-Policy; DH.nrw* <br>

>***Zitationsvorschlag nach TULLU-Regel:***
>*OER Policy‐Karte und Karte der Netzwerkstellen in NRW; von Wenzel, Marko; Homp, Frank; [CC BY 4.0](https://creativecommons.org/licenses/by/4.0); Link führt zu [Twillo](https://www.twillo.de/edu-sharing/components/render/1b355de9-849c-44ab-a219-42c325748eee)*

---
<!-- 10 -->
##  infOERmiert ‐ Der OER‐Blog vom Netzwerk Landesportal ORCA.nrw.  
Der `Blog` enthält **kurze informative Beiträge rund um OER**, die ursprünglich in der zugangsbeschränkten Community of Practice auf ORCA.nrw veröffentlicht wurden. **Der Blog bleibt offen und wird fortlaufend erweitert**.
![](MaterialienIntros/Webseite_infOERmiert-Netzwerk-Landesportal_CCBY40.jpg)
***`Medienformat:`*** *Webseite, Ebook, PDF und HTML* ***`erstellt/bearbeitbar mit:`*** *Web-Editor* <br>
***`Niveaustufe(n):`*** *Einsteiger (Starter)* <br>
***`Praxiskategorie(n)`*** *OER finden; OER herstellen; Mit OER lernen; Mit OER lehren; OER einführen; OER managen; Über OER forschen* <br>
***`Metadaten:`*** *OER; ORCA.nrw; Materialtipp; Praxiswerkstatt; Creative Commons; CC-Lizenz; Lizenzhinweis; OER-Policy; OER-Content*

> ***Zitationsvorschlag nach TULLU-Regel:***   
> *infOERmiert ‐ Der OER‐Blog vom Netzwerk Landesportal ORCA.nrw. Netzwerk Landesportal ORCA.nrw; von Urheber; [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/); Link führt zum [OERSI](https://oersi.org/resources/aHR0cHM6Ly9saW5kYWhhbG0taHNiaS5naXRodWIuaW8vaW5mT0VSbWllcnQ=)*

---

## Selbstlern-Materialien

---

<!-- 02 -->
### OER‐Glossar   
Dieses `Nachschlagewerk` erläutert **52 zentrale Begriffe** rund um das Thema Open Educational Resources (OER). <br> 
Stand: August 2023 
![](MaterialienIntros/Selbstlernkurs_OER-Glossar_CCBY40.jpg)
***`Medienformat:`*** *Selbstlernkurs* ***`erstellt/bearbeitbar mit:`*** *ILIAS; Moodle; HTML* <br>
***`Niveaustufe(n):`*** *Einsteiger (Starter); Praktiker; Experte* <br>
***`Praxiskategorie(n)`*** *n.a.* <br>
***`Metadaten:`*** *Urheberrecht; Werk; Barrierefreiheit; Zitat; Untertitel; Creative Commons; Lizenz; CC; Lehre, Repositorium*

> ***Zitationsvorschlag nach TULLU-Regel:***   
> *OER‐Glossar; von Gödecke, Svenja; Halm, Linda; Homp, Frank; Kobusch, Alexander; Schaffeld, Laura; Spaude, Magdalena; Weber, Tassja; [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/); Link führt zum [ILIAS der Uni zu Köln](https://www.edulabs.uni‐koeln.de/goto.php?target=crs_2218&client_id=iliasedulabs)*

---
<!-- 08 -->
### Learning Snacks: "ORCA.nrw: A University Network for OER 
`Lernspiel` `Edu-Game`
The example is based on a German network. You can find out **how the network works** and how it **advises on OER** together with the teacher Dr Jamal Groenstein, who gets to know the network as a protagonist. 
![](MaterialienIntros/Selbstlernkurs_LearningSnack_ORCAnrw-UniversityNetwork-for-OER_CCBYSA40.jpg) 
***`Medienformat:`*** *interaktive Web-Anwendung* ***`erstellt/bearbeitbar mit:`*** *Webanwendung [LearningSnacks](https://www.learningsnacks.de)* <br>
***`Niveaustufe(n):`*** *Einsteiger (Starter); Praktiker* <br>
***`Praxiskategorie(n)`*** *OER finden; OER herstellen; mit OER lernen; mit OER lehren; OER einführen; OER managen*<br>
***`Metadaten:`*** *OER; OER consultation; OER network; University; Higher Education*
> ***Zitationsvorschlag nach TULLU-Regel:***   
> *Learning Snacks: "ORCA.nrw: A University Network for OER"; von *Eube, Cornelia; Kobusch, Alexander; Niemann, Andrea; Nitzsche, Sina; Scherer, Elisabeth; Spaude, Magdalena*; [CC BY‐SA 4.0](https://creativecommons.org/licenses/by‐sa/4.0/); Link führt zu *[Learning Snacks](https://www.learningsnacks.de/share/218584/)*

---
<!-- 09 -->
### OER‐Wissenspool
Der `Selbstlernkurs` vermittelt in fünf Kategorien **Basiswissen zu Open Educational Resources** mit NRW-spezifischen Empfehlungen. Zudem enthält er eine OER-Bibliothek und einen Bereich für **OER-Showcases**. Der Kurs kann auf die eigene Insitution angepasst werden. Es stehen **Installationsanleitungen** zur Einbindung ins eigene LMS zur Verfügung.
![](MaterialienIntros/Selbstlernkurs_OER‐Wissenspool_CCBY40.jpg)
***`Medienformat:`*** Selbstlernkurs ***`erstellt/bearbeitbar mit:`*** *Moodle, Ilias; H5P* <br>
***`Niveaustufe(n):`*** *Einsteiger (Starter); Praktiker <br>
***`Praxiskategorie(n)`*** *OER finden: OER herstellen; Mit OER lernen; Mit OER lehren* <br>
***`Metadaten:`*** *OER erstellen; H5P; OER Basiswissen; OER-Supportmaterial*

> ***Zitationsvorschlag nach TULLU-Regel:***   
> *OER‐Wissenspool; von Nitzsche, Sina; Halm, Linda; [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/); Link führt zu [Ursprungsort](https://www.twillo.de/edu-sharing/components/render/2345cca5-7ef3-4a5c-90cb-1433b3401b47)*

---

## Textdokumente

---

<!-- 03 -->
### Praxisleitfaden: Aufzeichnung von Online‐Konferenzbeiträgen als OER    
Das `Textdokument` gibt **Vortragenden** wertvolle Tipps und Tricks für die **Vorbereitung, Durchführung** und **Nachbereitung** einer digitalen Veranstaltung, die aufgezeichnet werden und anschließend als OER veröffentlicht werden kann.
![](MaterialienIntros/Textdokument_Aufzeichnung-Online‐Konferenzbeitraege_OER_CCBY40.jpg)
***`Medienformat:`*** *Textdokument* ***`erstellt/bearbeitbar mit:`*** *MS Word* <br>
***`Niveaustufe(n):`*** *Einsteiger (Starter); Praktiker* <br>
***`Praxiskategorie(n)`*** *OER herstellen; OER einführen; OER managen* <br>
***`Metadaten:`*** *Online-Veranstaltung; Hochschuldidaktik; Leitfaden; Videoproduktion; OER-Fachtag; Konferenzorganisation; Dokumentation; Digitalisierung*

> ***Zitationsvorschlag nach TULLU-Regel:***   
> *Aufzeichnung von Online‐Konferenzbeiträgen als OER: Ein Praxisleitfaden; von Geurden, Bianca; Görlich, Sarah; Hützen, Nicole; Jahn, Markus; Méndez Parente, Josefine; Nitzsche, Sina; [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/); Link führt zu [Twillo](https://www.twillo.de/edu-sharing/components/render/d7d698e4-d9e9-47fb-87e4-86283206c982)*

---
<!-- 04 -->
### Checkliste: Open Educational Resources erstellen (v2.0) 
Der Zweck dieses `Textdokuments` / Leitfadens ist, Lehrenden eine **Orientierung** zu geben, welche **rechtlichen Maßgaben** Sie einhalten müssen und nach welchen **Qualitätsmerkmalen** Sie OER-Materialien entwickeln und beurteilen können.
![](MaterialienIntros/Textdokument_Checkliste-OER-erstellen-v2-0_CCBY40.jpg)
***`Medienformat:`*** *PDF; Textdokument* ***`erstellt/bearbeitbar mit:`*** *MS Word* <br>
***`Niveaustufe(n):`*** *Einsteiger (Starter); Praktiker*<br>
***`Praxiskategorie(n)`*** *OER herstellen*<br>
***`Metadaten:`*** *OER; Urheberrecht; Barrierefreiheit; Persönlichkeitsrecht; Produktion, Qualität*

> ***Zitationsvorschlag nach TULLU-Regel:***   
> *Checkliste Open Educational Resources erstellen (v2.0); von Kobusch,Alexander; Halm, Linda; [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/); Link führt zu [Twillo](https://www.twillo.de/edu-sharing/components/render/6c1f1da2-7ff6-4dd6-b87b-0404b980cc50)*
---
<!-- 06 -->
### Handreichung: Veröffentlichung von Lehr‐Lern‐Materialien als OER
Das `Textdokument` wurde für Lehrende der HHU erstellt, kann aber **leicht für andere (Hochschul-) Kontexte angepasst werden**. Es enthält **kompakte Informationen** zu Creative-Commons-Lizenzen und **Tipps** rund um das Urheberrecht zur Publikation von Materialien als OER.
![](MaterialienIntros/Textdokument_Veroeffentlichung-LLM-alsOER_CCBYSA40.jpg)
***`Medienformat:`*** *Textdokument; PDF* ***`erstellt/bearbeitbar mit:`*** *MS Word* <br>
***`Niveaustufe(n):`*** *Praktiker<br>
***`Praxiskategorie(n)`*** *OER herstellen*<br>
***`Metadaten:`*** *OER; Creative Commons; Lehrmaterialien; E-Learning; Open Educational Resources*

> ***Zitationsvorschlag nach TULLU-Regel:***   
> *Veröffentlichung von Lehr‐Lern‐Materialien als OER; von Scherer, Elisabeth; [CC BY‐SA 4.0](https://creativecommons.org/licenses/by‐sa/4.0/); Link führt zu *[Twillo](https://www.twillo.de/edusharing/components/render/53d9ee69‐384c‐4ddb‐bfc3‐a906197f5252)*

---
<!-- 05 -->
### Handreichung: Schwerpunkt Nutzung und Einbettung von nicht offen lizenzierten Materialien 
Der Schwerpunkt des `Textdokuments` liegt auf dem **Nutzen und Einbetten von nicht offen lizensierten Materialien**, die damit zunächst nicht ausdrücklich zur freien Weiterverwendung freigegeben sind. Die Handreichung ist an alle gerichtet, die OER-Material erstellen und diese auf einer (evtl. öffentlich zugänglichen) Plattform **veröffentlichen** wollen.
![](MaterialienIntros/Textdokument_Erstellung-OER‐Materialien-ORCAnrw_CCBY40.jpg)
***`Medienformat:`*** *PDF* ***`erstellt/bearbeitbar mit:`*** *PDF-Editor* <br>
***`Niveaustufe(n):`*** *Praktiker <br>
***`Praxiskategorie(n)`*** *OER herstellen* <br>
***`Metadaten:`*** *Handreichung; Landesportal ORCA.nrw; Material erstellen; Creative-Commons-Lizenz; Lizenz vergeben; CC-Lizenz*

> ***Zitationsvorschlag nach TULLU-Regel:***   
> *Handreichung zur Erstellung von OER‐Materialien für ORCA.nrw - Schwerpunkt: Nutzung und Einbettung von nicht offen lizenzierten Materialien; von Josupeit, Christina; Funk, Christian; Anderheide, Marie-Sophie; Meyer, Elisabeth [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/); Link führt zu [Twillo](https://www.twillo.de/edu-sharing/components/render/1ead1f94-6298-41e6-92c0-d11c30bb19a3)*


---

## Vorträge / Interviews

---
<!-- 07 -->
### 33 Minuten für… Das Konzept der Open Educational Resources (OER)  
Im `Video` zum Vortragsformat der **Coffee Lectures** lernen Sie das **Konzept von OER** kennen, erfahren, wo Sie **OER finden** und wie Sie selber die **eigenen Lehrmaterialien mit einer Creative-Commons-Lizenz teilen**.
![](MaterialienIntros/Video_Coffee_Lectures_Konzept-OER_CCBY40.jpg)
***`Medienformat:`*** FORMAT z.B. *Video* ***`erstellt/bearbeitbar mit:`*** *Schnittprogrammen* <br>
***`Niveaustufe(n):`*** *Einsteiger (Starter) <br>
***`Praxiskategorie(n)`*** OER finden; OER herstellen; OER einführen* <br>
***`Metadaten:`*** *Creative Commons Lizenzen; CC-Lizenzen*

> ***Zitationsvorschlag nach TULLU-Regel:***   
> *Coffee Lectures: 33 Minuten für… Offene Lehrmaterialien ‐ "Lehrmaterialien anderer nutzen und eigene teilen ‐ Das Konzept der Open Educational Resources (OER)"; von Spaude, Magdalena; [CC BY 4.0](https://creativecommons.org/licenses/by/4.0); Link führt zu [Twillo](https://www.twillo.de/edusharing/components/render/34a21631‐2963‐4a0c‐a97d‐4c2ed9a1d751)*

---


---

## Konferenzbeiträge

---


---

## Artikel in (Fach-)Zeitschriften

---
<!-- 11 -->
<!-- 12 -->
<!-- 13 -->
<!-- 14 -->
<!-- 15 -->
<!-- 16 -->
<!-- 17 -->
<!-- 18 -->
<!-- 19 -->
<!-- 20 -->
<!-- 21 -->
<!-- 22 -->
<!-- 23 -->
<!-- 24 -->
<!-- 25 -->
<!-- 26 -->
<!-- 27 -->
<!-- 28 -->
<!-- 29 -->
<!-- 30 -->
<!-- 31 -->
<!-- 32 -->
<!-- 33 -->
<!-- 34 -->
<!-- 35 -->
<!-- 36 -->
<!-- 37 -->
<!-- 38 -->
<!-- 39 -->
<!-- 40 -->
<!-- 41 -->
<!-- 42 -->





---

![grafik](https://github.com/user-attachments/assets/6e5b7a53-43ee-4dd4-b4a0-87c5a645cc04)



### hier gehts dann weiter (aktuell Sammelkiste)
 
a) Placeholder with link to Youtube

[![Entwicklungsumgebung mit Groovy/Git testen](https://img.youtube.com/vi/fbZOii_l7M4/maxresdefault.jpg)](https://youtu.be/fbZOii_l7M4)

b) AV-Portal player embedded

<iframe width="560" height="315" scrolling="no" src="//av.tib.eu/player/40456" frameborder="0" allowfullscreen="allowfullscreen"></iframe>

c) Youtube embedded

<iframe width="420" height="315"
src="https://www.youtube.com/embed/fbZOii_l7M4" allowfullscreen="allowfullscreen">
</iframe>


---

-->

# Impressum
This template for OER courses is released under MIT. The content of the document is subject to the respective license as indicated at the end of the generated files or in the metadata.yml.

<article>



### Haftung für Links

Unser Angebot enthält Links zu externen Webseiten Dritter, auf deren Inhalte wir keinen Einfluss haben.
Deshalb können wir für diese fremden Inhalte auch keine Gewähr übernehmen.
Für die Inhalte der verlinkten Seiten ist stets der jeweilige Anbieter oder Betreiber der Seiten verantwortlich.
Die verlinkten Seiten wurden zum Zeitpunkt der Verlinkung auf mögliche Rechtsverstöße überprüft.
Rechtswidrige Inhalte waren zum Zeitpunkt der Verlinkung nicht erkennbar.
Eine permanente inhaltliche Kontrolle der verlinkten Seiten ist jedoch ohne konkrete Anhaltspunkte einer Rechtsverletzung nicht zumutbar.
Bei Bekanntwerden von Rechtsverletzungen werden wir derartige Links umgehend entfernen.

### Urheberrecht

ERstmal unterliegt der Inhalt dem deutschen Urheberrecht.
Die Vervielfältigung, Bearbeitung, Verbreitung und jede Art der Verwertung außerhalb der Grenzen des Urheberrechtes bedürfen der schriftlichen Zustimmung des jeweiligen Autors bzw. Erstellers.
Downloads und Kopien dieser Seite sind nur für den privaten, nicht kommerziellen Gebrauch gestattet.
Soweit die Inhalte auf dieser Seite nicht vom Betreiber erstellt wurden, werden die Urheberrechte Dritter beachtet.
Insbesondere werden Inhalte Dritter als solche gekennzeichnet.Sollten Sie trotzdem auf eine Urheberrechtsverletzung aufmerksam werden, bitten wir um einen entsprechenden Hinweis.
Bei Bekanntwerden von Rechtsverletzungen werden wir derartige Inhalte umgehend entfernen.

</article>
