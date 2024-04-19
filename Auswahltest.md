<!--
author:   Your Name

email:    your@mail.org

icon:     img/icon.png

version:  0.0.1

language: de

narrator: US English Female

comment:  Try to write a short comment about
          your course, multiline is also okay.

link:     style.css

script:   https://cdnjs.cloudflare.com/ajax/libs/PapaParse/5.3.1/papaparse.min.js

@onload

const baseURL = (new URL("img", window.location.search.substr(1))).href

window["fish"] = {
  "body.typical": null,
  "body.flattened": null,
  "body.long": null,

  "mouth.inferior": null,
  "mouth.superior": null,
  "mouth.elongated": null,
  "mouth.terminal": null,

  "barbel.one": null,
  "barbel.several": null,
  "barbel.absent": null,

  "sucking_disc.present": null,
  "sucking_disc.absent": null,

  "color.black": null,
  "color.blue": null,
  "color.brown": null,
  "color.green": null,
  "color.grey": null,
  "color.red": null,
  "color.silver": null,
  "color.white": null,
  "color.yellow": null,

  "pattern.circles": null,
  "pattern.dots": null,
  "pattern.irregular": null,
  "pattern.spots": null,
  "pattern.stripes": null,
  "pattern.uniform": null,

  "fin.dorsal.one": null,
  "fin.dorsal.two": null,
  "fin.dorsal.three": null,
  "fin.dorsal.with_adipose": null,
  "fin.dorsal.with_finlets": null,
  "fin.dorsal.with_spines": null,

  "fin.pelvic.pelvic": null,
  "fin.pelvic.pectoral": null,
  "fin.pelvic.jugular": null,
  "fin.pelvic.absent": null,

  "fin.caudal.forked": null,
  "fin.caudal.straight": null,
  "fin.caudal.rounded": null,
  "fin.caudal.pointed": null,
  "fin.caudal.not_symmetric": null,
}

window["button"] = function(title, active, image) {
  const color = active ? '#f0842c' : "black" 
  return `<div style="padding: 8px; color: ${color}">
    <h4>${title}</h4>
    <img src="${image}" loading="lazy">
  </div>`
}

window.fish_filter = function() {
  if (window.fish) {
    let items = []
    for (const [item, selected] of Object.entries(window.fish)) {
      if (selected) {
        items.push(item)
      }
    }

    let result_often = []
    let result_seldom = []

    for (const fish of window.fish_db) {      
      let rslt = true

      for (const item of items) {
        if (!fish[item]) {
          rslt = false
          break
        }
      }

      if (rslt) {
        console.log("ssssssssssssssssss", fish["amount.often"])
        if (fish["amount.often"]) {
          result_often.push(fish.name)
        } else {
          result_seldom.push(fish.name)
        }
      }
    }

    const div = document.getElementById("results")

    if (div) {
      let list = ""

      if (result_often.length > 0) {
        list += "<br><h3>Häufig und regelmäßig in der Ostsee</h3>"
      }

      for(const fish of result_often) {
        let url = fish.toLocaleLowerCase().replace(/ /g, "-")
        let url_ = 
        list += `<a style="display: inline-flex; padding: 1rem; margin: 1rem; border: 1px solid black" href="#${url}"><span><h4>${fish}</h4><img src="${baseURL}/${url.replace(/ä/g, "ae").replace(/ö/g, "oe").replace(/ü/g, "ue").replace(/ß/g, "ss")}/thumbnail.png"></span></a>`
      }

      if (result_seldom.length > 0) {
        list += "<h3>Selten und als Irrgast in der Ostsee</h3>"
      }

      for(const fish of result_seldom) {
        let url = fish.toLocaleLowerCase().replace(/ /g, "-")
        let url_ = 
        list += `<a style="display: inline-flex; padding: 1rem; margin: 1rem; border: 1px solid black" href="#${url}"><span><h4>${fish}</h4><img src="${baseURL}/${url.replace(/ä/g, "ae").replace(/ö/g, "oe").replace(/ü/g, "ue").replace(/ß/g, "ss")}/thumbnail.png"></span></a>`
      }

      div.innerHTML = list
    }
  }
}

const CSV=`name,color.green,fin.dorsal.two,fin.dorsal.with_adipose,fin.caudal.forked,color.red,amount.often,pattern.uniform,color.brown,fin.dorsal.one,fin.pelvic.jugular,barbel.absent,fin.dorsal.with_spines,body.typical,color.silver,mouth.superior,body.flattened,pattern.dots,fin.dorsal.three,pattern.irregular,sucking_disc.present,fin.pelvic.pelvic,color.black,fin.caudal.pointed,fin.caudal.not_symetric,fin.pelvic.pectoral,color.grey,mouth.terminal,fin.caudal.straight,color.blue,pattern.spots,sucking_disc.absent,body.long,barbel.one,fin.pelvic.absent,fin.caudal.rounded,pattern.circles,color.yellow,mouth.elongated,pattern.stripes,fin.dorsal.with_finlets,mouth.inferior,barbel.several,color.white
Aal,,,,,,true,true,true,true,,true,,,true,true,,,,,,,true,true,,,true,true,,,,true,true,,true,,,true,,,,,,true
Aalmutter,,,,,,true,,true,true,true,true,,,,,,,,,,,true,true,,,true,true,,,true,true,true,,,,,true,,true,,,,
Adlerfisch,,true,,,,false,true,true,true,,true,,true,true,,,,,,,,true,,,true,true,true,true,,,true,,,,,,,,,,,,
Ährenfisch,,true,,true,,true,true,,,,true,,true,true,true,,,,,,,,,,true,,,,true,,true,,,,,,,,,,,,
Aland,,,,true,true,true,true,true,true,,true,,true,true,,,,,,,true,,,,,true,true,,,,true,,,,,,,,,,,,
Atlantischer Stör,,,,,,false,true,true,true,,,,true,,,,,,,,true,,,true,,true,,,,,true,true,,,,,,,,,true,true,true
Bachschmerle,,,,,,true,,true,true,,,,true,,,,,,true,,true,true,,,,true,,true,,true,true,true,,,,,,,,,true,true,true
Barbe,,,,true,true,false,true,true,true,,,,true,,,,,,,,true,,,,,true,,,,,true,,,,,,true,,,,true,true,true
Bitterling,true,,,true,true,false,true,true,true,,true,,true,true,,,,,,,true,,,,,true,true,,true,,true,,,,,,true,,true,,true,,
Blauer Wittling,,,,true,,true,true,,,true,true,,true,true,true,,,true,,,,,,,,,true,true,true,,true,,,,,,,,,,,,true
Blauhai,,true,,,,false,true,,,,true,,true,,,,,,,,true,,,true,,true,,,true,,true,,,,,,,,,,true,,true
Brachsen,,,,true,,true,true,,true,,true,,true,true,,,,,,,true,,,,,true,true,,,,true,,,,,,,,,,true,,
Brachsenmakrele,,,,true,,false,true,,true,,true,,true,true,true,,,,,,,true,,,true,true,true,,,,true,,,,,,,,,,,,
Brandbrassen,,,,true,,false,true,true,true,,true,,true,true,,,,,,,,,,,true,true,true,,,,true,,,,,,true,,true,,,,
Buckellachs,,,true,true,true,false,,true,,,true,,true,true,,,true,,,,true,,,,,true,true,true,true,,true,,,,,,,,,,,,
Butterfisch,,,,,,true,,true,true,true,true,,,,,,,,,,,true,,,,true,true,,,true,true,true,,,true,true,,,,,,,
Chagrinrochen,,true,,,,false,true,true,,,true,,,,,true,true,,,,true,true,true,,true,true,,,,true,true,,,,,true,,,,,true,,true
Conger,,,,,,false,true,,true,,true,,,true,,,,,,,,,true,,,true,,,,,true,true,,true,,,,,,,true,,true
Dicklippige Meeräsche,,true,,true,,true,true,,,,true,,true,true,,,,,,,,,,,true,true,true,,true,,true,,,,,,,,true,,,,
Döbel,,,,true,true,false,,true,true,,true,,true,true,,,,,,,true,,,,,true,true,,,,true,,,,,,true,,,,,,
Doggerscharbe,,,,,,false,true,true,true,true,true,,,,,true,true,,true,,,,,,,true,true,,,,true,,,,true,,,,,,,,true
Dorsch,true,,,,,true,,true,,true,,,true,,,,true,true,true,,,,,,,,,true,,,true,,true,,,,true,,,,true,,true
Dreistachliger Stichling,true,,,,true,true,true,true,,,true,true,true,true,,,,,,,true,,,,true,true,true,true,,,true,,,,,,,,,,,,true
Dünnlippige Meeräsche,,true,,true,,true,true,,,,true,,true,true,,,,,,,,,,,true,true,true,,true,,true,,,,,,,,,,,,
Einfarbiger Pelamide,,true,,true,,false,true,,,,true,,true,true,,,,,,,,,,,true,true,true,,true,,true,,,,,,,,,true,,,true
Finte,,,,true,,false,true,,true,,true,,true,true,,,,,,,true,true,,,,true,true,,true,true,true,,,,,,,,,,,,
Fleckengrundel,,true,,,true,true,,true,,,true,,true,,true,,true,,true,true,,true,,,true,true,true,,true,true,,,,,true,,true,,true,,,,true
Fleckhai,,true,,,,false,,true,,,true,,true,,,,,,true,,true,true,,true,,,,,,true,true,,,,,,,,,,true,,true
Flunder,,,,,true,true,true,true,true,true,true,,,,,true,,,true,,,true,,,,true,true,,,true,true,,,,true,,,,,,,,true
Flussbarsch,,true,,true,true,true,,true,,,true,,true,,,,,,,,,true,,,true,true,true,,,,true,,,,,,true,,true,,,,
Flussneunauge,,true,,,,true,true,,,,true,,,true,,,,,true,,,true,true,,,true,,,,,true,true,,true,,,,,,,true,,true
Franzosendorsch,,,,,,false,true,true,,true,,,true,true,,,,true,,,,true,,,,true,,true,,true,true,,true,,,,,,true,,true,,
Froschdorsch,,true,,,,true,true,true,,true,,,true,,,,,,,,,true,,,,,,,,,true,,true,,true,,,,,,true,,
Fuchshai,,true,,,,false,true,,,,true,,true,,,,,,,,true,,,true,,true,,,true,,true,,,,,,,,,,true,,true
Gabeldorsch,,true,,,,false,true,true,,true,,,true,,,,,,,,,,,,,true,,true,,,true,,true,,,,,,,,true,,true
Gabelmakrele,,,,true,,false,true,,,,true,true,true,true,,,,,,,,true,,,true,true,true,,,true,true,,,,,,,,,,,,true
Gefleckter Lippfisch,true,,,,true,true,,true,true,,true,,true,,,,true,,true,,,true,,,true,,true,true,,true,true,,,,true,,true,,true,,,,true
Gemeiner Dornhai,,true,,,,false,true,true,,,true,,true,,,,true,,,,true,,,true,,true,,,,,true,,,,,,,,,,true,,true
Gemeiner Seeteufel,,true,,,,false,true,true,,true,true,true,,,true,true,,,true,,,,,,,true,,true,,,true,,,,true,,,,,,,,true
Gemeine Seezunge,,,,,,true,true,true,true,true,true,,,,,true,true,,true,,,true,,,,true,,,,true,true,,,,true,,,,,,true,true,true
Gestreifeter Leierfisch,,true,,,,false,,true,,true,true,,true,,,,,,true,,,,,,,,true,true,true,true,true,,,,true,,true,,true,,true,,true
Gestreifter Seewolf,,,,,,false,,,true,,true,,true,,,,,,,,,true,,,,true,true,true,true,,true,true,,true,true,,,,true,,,,
Gewöhnlicher Stechrochen,,,,,,false,true,true,,,true,true,,,,true,,,,,true,true,true,,true,true,,,,,true,,,,,,,,,,true,,true
Giebel,,,,true,,false,true,true,true,,true,,true,true,,,,,,,true,,,,,true,true,,true,,true,,,,,,true,,,,,,
Glasgrundel,,true,,,,true,true,,,,true,,true,,true,,true,,,true,,true,,,true,true,true,true,,,,,,,true,,,,,,,,true
Glattbutt,,,,,,true,,true,true,true,true,,,,,true,true,,true,,,true,,,,true,true,,,true,true,,,,true,,true,,,,,,
Glattrochen,,true,,,,false,,true,,,true,,,,,true,true,,true,,true,true,true,,,true,,,,true,true,,,,,true,true,,,,true,,true
Goldmaid,true,,,,true,true,,true,true,,true,,true,,,,,,true,,,true,,,true,,true,true,,true,true,,,,true,,true,,true,,,,
Goldmeeräsche,,true,,true,,false,true,,,,true,,true,true,,,,,,,,,,,true,true,true,,,,true,,,,,,true,,,,,,
Graskarpfen,,,,true,,false,true,true,true,,true,,true,,,,,,,,true,,,,,true,true,,,,true,,,,,,,,,,,,true
Grasnadel,true,,,,,true,true,true,true,,true,,,,true,,,,,,,,,,,,,,,true,true,true,,true,true,,true,true,true,,,,
Grauer Knurrhahn,,true,,true,true,true,true,true,,,true,,true,true,,,,,true,,true,true,,,true,true,,true,,,true,,,,,,,,,,true,,true
Grauhai,,,,,,false,true,true,true,,true,,true,,,,,,,,true,,,true,,true,,,,,true,,,,,,,,,,true,,true
Grosser Sandaal,,,,true,,true,true,,true,,true,,,true,true,,,,,,,true,,,,true,true,,true,true,true,true,,true,,,,,,,,,
Großer Scheibenbauch,,,,,,true,true,true,true,,true,,true,,,,,,true,true,,,,,true,true,,,,true,,,,,true,,true,,true,,true,,true
Grosse Schlangennadel,,,,,true,false,,true,true,,true,,,true,true,,,,true,,,,true,,,true,,,true,true,true,true,,true,true,,true,true,true,,,,
Grosse Seenadel,true,,,,true,true,true,true,true,,true,,,,true,,,,,,,,,,,true,,,,true,true,true,,true,true,,true,true,true,,,,
Gründling,,,,true,,false,,true,true,,,,true,,,,true,,,,true,true,,,,,,,true,true,true,,,,,,true,,,,true,true,
Güster,,,,true,true,true,true,,true,,true,,true,true,,,,,,,true,,,,,true,true,,,,true,,,,,,,,,,true,,
Haarbutt,,,,,,true,,true,true,true,true,,,,,true,true,,true,,,true,,,,true,true,,,true,true,,,,true,true,,,,,,,true
Hasel,,,,true,true,false,true,true,true,,true,,true,true,,,,,,,true,,,,,true,,,,,true,,,,,,,,,,true,,
Hecht,true,,,true,,true,,true,true,,true,,true,,,,true,,true,,true,,,,,,true,,,true,true,true,,,,,true,true,true,,,,true
Heilbutt,,,,,,false,true,true,true,true,true,,,,,true,,,,,,,,,,true,true,true,,,true,,,,,,,,,,,,true
Hering,,,,true,,true,true,,true,,true,,true,true,true,,,,,,true,true,,,,,,,true,,true,,,,,,,,,,,,
Heringshai,,true,,,,false,true,,,,true,,true,,,,,,,,true,true,,true,,true,,,true,,true,,,,,,,,,,true,,true
Heringskönig,,true,,,,false,,true,true,,true,,true,,true,,,,true,,,true,,,true,true,,,,true,true,,,,true,true,true,,,,,,
Hornhecht,true,,,true,,true,true,,true,,true,,,true,,,,,,,true,,,,,true,,,true,,true,true,,,,,,true,,,,,
Hundszunge,,,,,,false,true,true,true,true,true,,,,,true,true,,true,,,,,,,true,true,,,,true,,,,true,,,,,,,,true
Karausche,,,,true,,true,true,true,true,,true,,true,true,,,,,,,true,,,,,true,true,true,,true,true,,,,,,true,,,,,,
Karpfen,true,,,true,,false,true,true,true,,,,true,,,,,,,,true,,,,,true,true,,,,true,,,,,,true,,,,,true,
Kaulbarsch,,,,true,,true,,true,true,,true,,true,,,,true,,,,,true,,,true,,true,,,true,true,,,,,,true,,,,,,true
Kleine Maräne,,,true,true,,true,true,,,,true,,true,true,true,,,,,,true,,,,,,,,,,true,,,,,,,,,,,,
Kleiner Sandaal,true,,,true,,false,true,,true,,true,,,true,true,,,,,,,,,,,true,true,,true,,true,true,,true,,,,,,,,,
Kleiner Scheibenbauch,,,,,true,false,true,true,true,,true,,true,,,,,,true,true,,,,,true,true,true,,,true,,,,,true,,true,,true,,,,true
Kleine Schlangennadel,true,,,,true,true,true,true,true,,true,,,,true,,,,true,,,true,true,,,true,,,true,,true,true,,true,,,true,true,true,,,,
Kleine Seenadel,true,,,,,true,true,true,true,,true,,,,true,,,,,,,,,,,true,,,,true,true,true,,true,true,,true,true,true,,,,
Kleingefleckter Katzenhai,,true,,,,true,,true,,,,,true,,,,true,,,,true,true,,true,,,,,,true,,true,,,,,,,,,true,,true
Kliesche,,,,,true,true,true,true,true,true,true,,,,,true,true,,,,,,,,,true,true,,,true,true,,,,true,,,,,,,,true
Klippenbarsch,true,,,,true,true,true,true,true,,true,,true,,,,,,,,,,,,true,true,true,true,,true,true,,,,true,,,,,,,,true
Köhler,true,,,true,,true,true,true,,true,true,,true,,true,,,true,,,,,,,,true,,,true,,true,,true,,,,,,,,,,
Lachs,,,true,true,,true,,true,,,true,,true,true,,,true,,,,true,true,,,,true,true,true,true,,true,,,,,,true,,true,,,,
Lammzunge,,,,,,false,,true,true,true,true,,,,,true,,,true,,,,,,,true,true,,,true,true,,,,true,,,,,,,,true
Langflossen Brachsenmakrele,,,,true,,false,true,,true,,true,,true,true,true,,,,,,,true,,,true,true,true,,,,true,,,,,,,,,,,,
Leng,,true,,,,false,true,true,,true,,,true,,,,,,,,,,,,,true,true,,,,true,true,true,,true,,true,,,,,,true
Maifisch,,,,true,,false,true,,true,,true,,true,true,,,,,,,true,true,,,,true,true,,true,true,true,,,,,,,,,,,,
Makrele,,,,true,,true,,,,,true,,true,true,,,,,,,,true,,,true,true,true,,true,,true,,,,,,,,true,true,,,true
Makrelenhecht,true,,,true,,false,true,,,,true,,,true,,,,,,,true,,,,,true,,,,,true,true,,,,,,true,,true,,,true
Marmorkarpfen,,,,true,,false,true,true,true,,true,,true,true,true,,,,true,,true,true,,,,true,,,,,true,,,,,,,,,,,,true
Meerengel,,true,,true,,false,,true,,,true,,,,,true,,,true,,true,true,,true,,true,true,,,,true,,,,,,,,,,,,true
Meerforelle,,,true,true,true,true,,true,,,true,,true,true,,,true,,,,true,true,,,,true,true,true,true,,true,,,,,,true,,,,,,
Meerneunauge,,true,,,,true,,,,,true,,,,,,,,true,,,true,true,,,true,,,true,true,true,true,,true,,,true,,,,true,,true
Moderlieschen,,,,true,,true,true,,true,,true,,true,true,true,,,,,,true,,,,,true,,,true,,true,,,,,,true,,,,,,
Mondfisch,,,,,,false,true,true,true,,true,,true,true,,,,,,,,,,,,true,true,,,true,true,,,true,true,,,,,,,,true

`

Papa.parse(CSV, {
  quotes: false,
  header: true,
  dynamicTyping: true,
  complete: function(data){
    window.fish_db = data.data

    setTimeout(window.filter_fish, 2000)
  }
})

@end

@button
<script input="button" run-once="true" modify="false">
  function show () {
    if (window.fish && window.button) {
      if(window.fish["@0"] == null) {
        window.fish["@0"] = false
      } else {
        window.fish["@0"] = !window.fish["@0"]
        window.fish_filter()
      }
      send.html(window.button("@1", window.fish["@0"], "@2"))

    } else {
      setTimeout(function() {
        show()
      }, 100);  
    }  
  }

  show()
</script>
@end

-->


# Netzwerk ORCA.nrw 
a) Contentbuffet: Praxiskategorien 
c) Level
c) Medienart, 



* [landing page](https://Steffi82.github.io/ORCA-Netzwerk-NRW/)

abc 

<!--
persistent: true
-->

<details>

<summary> Niveaustufe </summary>

__Niveaustufe__

@[button(body.typical,Einsteiger)](img/_button/body/long.png)
@[button(body.long,Praktiker)](img/_button/body/long.png)
@[button(body.flattened,Experte)](img/_button/body/flattened.png)


</details>

---

<details>

<summary> Praxiskategorie </summary>

__Praxiskategorie__

@[button(mouth.terminal,OER finden)](img/_button/mouth/terminal.png)
@[button(mouth.superior,OER herstellen)](img/_button/mouth/superior.png)
@[button(mouth.inferior,Mit OER lernen)](img/_button/mouth/inferior.png)
@[button(mouth.elongated,Mit OER lehren)](img/_button/mouth/elongated.png) 
@[button(mouth.elongated,OER einführen)](img/_button/mouth/elongated.png)
@[button(mouth.superior,OER managen)](img/_button/mouth/superior.png)
@[button(mouth.inferior,unterständig)](img/_button/mouth/inferior.png)

</details>


<summary> Medienart/-typ </summary>

__Barteln__

@[button(barbel.one,Video)](img/_button/barbel/one.png)
@[button(barbel.several,Audio)](img/_button/barbel/several.png)
@[button(barbel.absent,PDF)](img/_button/barbel/absent.png)



</details>

<div id="results"></div>

## Dorsch

![Dorsch in Seitenansicht](img/dorsch/1.jpg "©Timo Moritz/DMM")
![Dorsch in Vorderansicht](img/dorsch/2.jpg "©Timo Moritz/DMM")
![Dorschkopf in Seitenansich](img/dorsch/3.jpg "©Timo Moritz/DMM")

<article class="main-info">

_D-Dorsch, Kabeljau;_
_GB-Cod; DK-Torsk;_
_PL-Dorz; LT-Mence;_
_LV-Menca;_
_EST-Tursk;_
_RU-Атлантическая треска;_
_FIN-Turska;_
_S-Torsk_

### Erkennungsmerkmale

![Dorsch schematische Zeichnung](img/dorsch/0.png)

1. Lange Bartel am Kinn.
2. Maul deutlich unterständig.
3. Seitenlinie deutlich hell hervorgehoben.

* 3 Rücken- und 2 Afterflossen.
* Hellbraun, gelblich oder grünlich mit markantem dunkelbraunem Fleckenmuster.
  Meist 40 bis 70 cm, früher bis 200 cm Länge und über 95 kg Gewicht.

### Ähnliche Arten

* [Wittling](#wittling) - Bartel sehr klein oder fehlend; Seitenlinie nicht weiß.
* [Schellfisch](#schellfisch) - Bartel kleiner; Seitenlinie nicht weiß; mit markantem schwarzen Fleck über der Brustflosse.
* [Franzosendorsch](#franzosendorsch) - Schnauze nur etwa so lang wie Augendurchmesser; Seitenlinie nicht weiß.
* [Zwergdorsch](#zwergdorsch) - Schnauze nur etwa so lang wie Augendurchmesser; Seitenlinie nicht weiß.

### Lebensweise

Meist in Schwärmen bodennah in bis zu 600 m Tiefe.
Laicht im Frühjahr mit bis zu 5 Millionen Eier pro Weibchen.
Jungfische meist in flacherem Wasser.
Die Lebensweisen der verschiedenen Stämme im Atlantik, der Ostsee und Pazifik unterscheidet sich stark.
In der Ostsee stellt das Bornholmer Becken während der Sommermonate den wichtigsten Laichgrund dar.
Lebenserwartung bis 25 Jahre.

### Ernährung

Kleinere Fische, wie Heringe und Sandaale, Krabben, Garnelen, Würmer und Muscheln.

### Bedeutung

Als beliebter Speisefisch kommerziell stark genutzt; in der Ostsee einer der wichtigsten Nutzfischarten.
Früher vor allem getrocknet als "Stockfisch" und "Klippfisch" gehandelt.

### Gefährdung

Bestände rückläufig; vor allem durch Fischerei, aber auch wegen Gewässerverschmutzung und Habitatzerstörung.

</article>

<!-- class="sub-info" -->
> #### Gadus morhua
>
> __Familie:__ Gadidae
>
> __Ordnung:__ Gadiformes
>
> ![Karte Verbreitungsgebiet](img/dorsch/map.png)
>
> __Verbreitung:__ Gesamte Ostsee, außer im nördlichen Bottnischen Meerbusen.
>
> __Häufigkeit:__ sehr häufig
>
> __Gefährdung:__ nicht gefährdet

## Seehase

![Seehase in Vorderansicht](img/seehase/1.jpg "©Timo Moritz/DMM")
![Seehase in Seitenansicht](img/seehase/2.jpg "©Timo Moritz/DMM")
![Seehase in Bauchansicht](img/seehase/3.jpg "©Timo Moritz/DMM")
![Seehase in Seitenansich](img/seehase/4.jpg "©Timo Moritz/DMM")

<article class="main-info">

_D-Seehase;_
_GB-Lumpsucker, Lumpfish;_
_DK-Stenbider;_
_PL-Tasza;_
_LT-Ciegorius;_
_LV-Zaķzivs;_
_EST-Merivarblane;_
_RU-Пинагор;_
_FIN-Rasvakala;_
_S-Sjurygg_

### Erkennungsmerkmale

![Dorsch schematische Zeichnung](img/seehase/0.png)

1. Reihen von Knochendornen auf Rücken und Flanken.
2. Bauchflossen sind zu einer Saugscheibe umgewandelt.

* Jungtiere mit zwei Rückenflossen; die erste wird während des Wachstums von einem Hautkamm umwachsen.
* Körper massig und hochrückig.
  Männchen meist 30 bis 40 cm, Weibchen meist über 50 cm, max. 61cm Länge; in der Ostsee meist kleiner bleibend.

### Ähnliche Arten

Unverwechselbar

### Lebensweise

Lebt auf steinigen bis felsigen Böden in 20 bis 200m, max. 400 m Tiefe, wo er sich mit seiner Saugscheibe festsaugen kann.
Laicht im Frühjahr, das Gelege von bis zu 350.000 Eiern wird vom Männchen bewacht.
Die Wintermonate verbringen sie in größeren Tiefen.

### Ernährung

Krebstiere, Rippenquallen und kleine Fische; gelegentlich pflanzliches Material.

### Bedeutung

Wirtschaftliche Bedeutung als Speisefisch; seine Eier werden als "deutscher Kaviar" gehandelt.

### Gefährdung

Vermutlich nicht gefährdet.

### Bermerkung

Meist sind Seehasen gräulich oder grünlich gefärbt, doch während der Fortpflanzungszeit werden die Männchen leuchtend rot.

</article>

<!-- class="sub-info" -->
> #### Cyclopterus lumpus
>
> __Familie:__ Cyclopteridae
>
> __Ordnung:__ Scorpaeniformes
>
> ![Karte Verbreitungsgebiet](img/seehase/map.png)
>
> __Verbreitung:__ Häufig in der gesamten Ostsee mit Ausnahme des finnischen und bottnischen Meerbusens.
>
> __Häufigkeit:__ sehr häufig
>
> __Gefährdung:__ nicht gefährdet

## Meerneunauge

![Meerneunauge in Seitenansicht auf dem Grund liegend](img/meerneunauge/1.jpg "©Andi Hartl")
![Meerneunauge in Seitenansicht](img/meerneunauge/2.jpg "©Andi Hartl")
![Meerneunauge in Seitenansicht auf dem Grund liegend](img/meerneunauge/3.jpg "©Andi Hartl")
![Neerneunauge Kopf mit Maul](img/meerneunauge/4.jpg "©Andi Hartl")

<article class="main-info">

_D-Meerneunauge;_
_GB-Sea lamprey, great sea lamprey, green sea lamprey;_
_DK-Havlempret;_
_PL-Minóg morski;_
_LT-Upinė nėgė;_
_LV-Jūras nēģis;_
_EST-Merisutt;_
_RU-Минога морская;_
_FIN-Merinahkiainen;_
_S-Havsnejonöga_

### Erkennungsmerkmale

![Meerneunauge schematische Zeichnung](img/meerneunauge/0.png)

1. Mundscheibe mit zahlreichen kleinen Hornzähne.

* 7 Kiemenöffnungen (pro Seite) und eine einzelne Nasenöffnung.
* Keine paarigen Flossen.
* Körper meist deutlich marmoriert.

Meist 70 bis 90 cm, selten bis 120 cm; etwa 5 cm im Durchmesser.

### Ähnliche Arten

* [Flussneunauge](#flussneunauge) - drei Paar große Hornzähne beiderseits der Maulöffnung; Körper einheitlich gefärbt; nur etwa daumendick.
* [Aal](#aal) - paarige Brustflossen; Kiemendeckel und nur eine äußere Kiemenöffnung.
* [Conger](#conger) - paarige Brustflossen; Kiemendeckel und nur eine äußere Kiemenöffnung.

### Lebensweise

Die laichreifen Erwachsenen wandern flussaufwärts.
Sie pflanzen sich nur einmal im Leben fort.
Die Larven, die sogenannten Querder, leben drei bis fünf Jahre in Sand- oder Schlammgrund eingegraben und ernähren sich filtrierend von Kleinstpartikeln.
Nach der Umwandlung zum Erwachsenen wandern sie zurück ins Meer und leben dort bis zur Geschlechtsreife etwa drei bis vier Jahre lang.

### Ernährung

Saugt sich mit der Mundscheibe an Fische an, um sich von deren Blut und kleingeraspelten Gewebe zu ernähren.
Kleinere Fische werden teilweise auch komplett gefressen.

### Bedeutung

Geschätzter Speisefisch; wegen seiner geringen Bestände jedoch kaum wirtschaftlich nutzbar.

### Gefährdung

Gefährdet durch Flussverbauung (z.B. Wasserkraftwerke) und Gewässerverschmutzung.

</article>

<!-- class="sub-info" -->
> #### Petromyzon marinus
>
> __Familie:__ Petromyzontidae
>
> __Ordnung:__ Petromyzontiformes
>
> ![Karte Verbreitungsgebiet](img/meerneunauge/map.png)
>
> __Verbreitung:__ Ostsee, mit Ausnahme des bottnischen Meerbusens
>
> __Häufigkeit:__ regelmäßig
>
> __Gefährdung:__ gefährdet

## Blauhai

![Blauhai im offenen Meer](img/blauhai/1.jpg "©Timo Moritz/DMM")
![Blauhai in Seitenansicht](img/blauhai/2.jpg "©Timo Moritz/DMM")
![Blauhai (Kopfausschnit) in Seitenansicht](img/blauhai/3.jpg "©Timo Moritz/DMM")

<article class="main-info">

_D-Blauhai;_
_GB-Blue shark, blue pointer;_
_DK-Blåhaj;_
_PL-Zarlacz blekitny;_
_LT-Melsvasis ryklys;_
_EST-Sinihai;_
_RU-Синяя акула;_
_FIN-Sinihai;_
_S-Blåhaj_

### Erkennungsmerkmale

![Blauhai schematische Zeichnung](img/blauhai/0.png)

1. Zweite Rückenflosse sehr viel kleiner als die erste.
2. Schwanzstiel ohne seitlichen Kiel.
3. Brustflosse endet deutlich vor der Rückenflosse.

* 5 Kiemenspalten, schlanker Körper.
* Rücken leuchtend blau (nach dem Tod zu grau erblassend), Bauch weiß.
  Meist unter 3 m, max. 3,8 m Länge

### Ähnliche Arten

* [Heringshai](#heringshai) - Körper deutlich massiger; Brustflosse endet unter dem Beginn der Rückenflosse, mit stark ausgebildetem seitlichen Schwanzkiel.
* [Gemeiner Dornhai](#gemeiner-dornhai) - mit Dornen an den Rückenflossen; ohne Afterflosse.

### Lebensweise

Lebt oberflächennah im offenen Meer und ist hauptsächlich nachtaktiv.
Nach einer Tragzeit von 9 bis 12 Monaten schwankt die Zahl der lebend geborenen Jungen sehr stark, zwischen 4 und 135 Stück.

### Ernährung

Vor allem Schwarmfisch wie Hering und Makrele, aber auch Kalmare, andere Wirbellose und gelegentlich kleinere Haie.

### Bedeutung

Beliebte Zielart von Sportanglern.
Als Speisefisch von geringer Bedeutung, jedoch häufig zur Gewinnung von Haiflossen gefangen.

### Gefährdung

Stark befischte Haiart; außerdem sehr häufiger Beifang von Langleinenfischerei, Schlepp- und Kiemennetzen.

</article>

<!-- class="sub-info" -->
> #### Prionace glauca
>
> __Familie:__ Carcharhinidae
>
> __Ordnung:__ Carchariniformes
>
> ![Karte Verbreitungsgebiet](img/blauhai/map.png)
>
> __Verbreitung:__ Irrgast in der westlichen Ostsee
>
> __Häufigkeit:__ sehr selten
>
> __Gefährdung:__ nicht gefährdet

## Flussneunauge

![Flussneunauge in Seitenansicht auf einem Stein liegend](img/flussneunauge/1.jpg "©Andi Hartl")
![Flussneunauge in Seitenansicht schwimmend](img/flussneunauge/2.jpg "©Andi Hartl")
![3 Flussneunaugen in Seitenansicht verschlungen](img/flussneunauge/3.jpg "©Andi Hartl")

<article class="main-info">

_D-Flussneunauge;_
_GB-River lamprey;_
_DK-Almindelig flodlampret;_
_PL-Minóg rzeczny;_
_LT-Upinė nėgė;_
_LV-Upes nēģis;_
_EST-Jõesilm;_
_RU-Речная минога;_
_FIN-Nahkiainen;_
_S-Flodnejonöga_

### Erkennungsmerkmale

![Flussneunauge schematische Zeichnung](img/flussneunauge/0.png)

1. Beiderseits der Mundöffnung drei große Hornzähne.

* Sieben Kiemenöffnungen (pro Seite) und eine einzelne Nasenöffnung.
* Keine paarigen Flossen.
* Körper ohne Musterung; bläulicher bis bräunlicher Rücken scharf vom hellen Bauch abgegrenzt.

Meist 30 bis 40 cm, selten bis 50 cm Länge; etwa daumendick.

### Ähnliche Arten

* [Meerneunauge](#meerneunauge) - sehr viele kleine Hornzähne auf der Mundscheibe; Körper meist marmoriert;
  deutlich größer und dicker werdend.
* [Aal](#aal) - paarige Brustflossen; Kiemendeckel und nur eine äußere Kiemenöffnung.
* [Conger](#conger) - paarige Brustflossen; Kiemendeckel und nur eine äußere Kiemenöffnung.

### Lebensweise

Die laichreifen Erwachsenen wandern flussaufwärts.
Sie pflanzen sich nur einmal im Leben fort.
Die Larven, die sogenannten Querder, leben bis zu vier Jahre in Sand- oder Schlammgrund eingegraben und ernähren sich filtrierend von Kleinstpartikeln.
Nach der Umwandlung zum Erwachsenen leben sie bis zur Geschlechtsreife etwa zwei Jahre im küstennahen Meer.

### Ernährung

Saugt sich mit der Mundscheibe an Fische an, um sich von deren Blut und kleingeraspeltem Gewebe zu ernähren.

### Bedeutung

Nur in wenigen Regionen von wirtschaftlicher Bedeutung, z.B. in Lettland.

### Gefährdung

Laichwanderungen werden durch Flussverbauungen (z.B. Wasserkraftwerke) stark behindert.
Durch ihre Langlebigkeit sind die Larven sehr empfindlich gegenüber Wasserverschmutzung.

</article>

<!-- class="sub-info" -->
> #### Lampetra fluviatilis
>
> __Familie:__ Petromyzontidae
>
> __Ordnung:__ Petromyzontiformes
>
> ![Karte Verbreitungsgebiet](img/flussneunauge/map.png)
>
> __Verbreitung:__ in der gesamten Ostsee, vor allem küstennah
>
> __Häufigkeit:__ regelmäßig
>
> __Gefährdung:__ gefährdet

## Heringshai

![Gefangener Heringshai auf Seite liegend](img/heringshai/1.jpg "PD: NOAA")

<article class="main-info">

_D-Heringshai;_
_GB-Porbeagle;_
_DK-Sildehaj;_
_PL-Lamna śledziowa;_
_EST-Harilik heeringahai;_
_RU-Атлантическая сельдевая акула;_
_FIN-Sillihai;_
_S-Håbrand_

### Erkennungsmerkmale

![Heringshai schematische Zeichnung](img/heringshai/0.png)

1. Zweite Rückenflosse sehr viel kleiner als die erste.
2. Schwanzstiel mit starkem seitlichen Kiel.
3. Brustflosse endet direkt unter der Rückenflosse.

* 5 Kiemenspalten, massiger Körper.
* Rücken dunkel- bis blau-grau, Bauch weiß.

Meist 2,2 bis 2,6 m, max. 3,7 m Länge und 200 kg Gewicht.

### Ähnliche Arten

* [Blauhai](#blauhai) - viel schlanker; Brustflosse endet deutlich vor dem Beginn der Rückenflosse; ohne Schwanzkiel.
* [Gemeiner Dornhai](#gemeiner-dornhai) - mit Dornen an den Rückenflossen; ohne Schwanzkiel; ohne Afterflosse.

### Lebensweise

Lebt oberflächennah im offenen Meer, gelegentlich auch bis in 700 m Tiefe.
Nach einer Tragzeit von 8 Monaten werden 1 bis 5 Junge mit bis zu 60 cm Länge geboren.
Die Jungen ernähren sich im Mutterleib von unbefruchteten Eiern.

### Ernährung

Vor allem Schwarmfische, wie Heringe und Makrelen, zuweilen aber auch Dornhaie, Dorsche und Plattfische.
Jagt gelegentlich in Gruppen.

### Bedeutung

Beliebter Speisefisch mit hoher wirtschaftlicher Bedeutung.

### Gefährdung

Durch seine langsame Reproduktionsrate und ungeregelte Fangraten gefährdet.
Häufiger Beifang bei Netz- und Langleinenfischerei.

</article>

<!-- class="sub-info" -->
> #### Lamna nasus
>
> __Familie:__ Lamnidae
>
> __Ordnung:__ Lamniformes
>
> ![Karte Verbreitungsgebiet](img/heringshai/map.png)
>
> __Verbreitung:__ sehr selten in der westlichen Ostsee, als Irrgast bis in die zentrale Ostsee
>
> __Häufigkeit:__ sehr selten
>
> __Gefährdung:__ nicht gefährdet

## Fuchshai

![Gefangener Fuchshai auf Seite liegend](img/fuchshai/1.jpg "PD: NOAA")
![Fuchshai beim Sprung aus dem Wasser](img/fuchshai/2.jpg "CC: Charmanderson/iNaturalist.org")
![Fuchshai schwimmend mit Angelhaken im Maul](img/fuchshai/3.jpg "PD: NOAA")

<article class="main-info">

_D-Fuchshai, Drescherhai;_
_GB-Tresher shark, common tresher;_
_DK-Rævehaj;_
_PL-Kosogon;_
_EST-Harilik rebashai;_
_RU-Обыкновенная морская лисица;_
_FIN-Kettuhai;_
_S-Rävhaj_

### Erkennungsmerkmale

![Fuchshai schematische Zeichnung](img/fuchshai/0.png)

1. Oberer Schwanzlappen erreicht etwa die Länge des restlichen Körpers. 

* Rückenfärbung variabel bläulich, gräulich, bräunlich bis schwärzlich; Bauch hell.

Männchen meist bis 4 m, Weibchen meist bis 5,5 m, max. 6 m Länge.

### Ähnliche Arten

### Lebensweise

Lebt oberflächennah in offen Meer und ist tagaktiv; Jungtiere sind häufiger in Küstennähe.
Nach 9 bis 12 Monaten Tragzeit werden 2 bis 4 Jungen lebend geboren.
Gilt als menschenscheu.

### Ernährung

Hauptsächlich von kleineren Schwarmfischen wie Makrelen und Heringen, jedoch auch Kalmaren und Krebstieren.

### Bedeutung

Hoher wirtschaftlicher Nutzen der Flossen und als Speisefisch.

### Gefährdung

Durch steigende wirtschaftliche Nutzung als weltweit gefährdet eingeschätzt.

</article>

<!-- class="sub-info" -->
> #### Alopias vulpinus
>
> __Familie:__ Alopiidae
>
> __Ordnung:__ Lamniformes
>
> ![Karte Verbreitungsgebiet](img/fuchshai/map.png)
>
> __Verbreitung:__ Sehr selten im Kattegat.
>
> __Häufigkeit:__ sehr selten
>
> __Gefährdung:__ gefährdet

## Glattrochen

<article class="main-info">

_D-Glattrochen;_
_GB-Common skate, blue skate;_
_DK-Skade;_
_PL-Płaszczka naga, raja gładka;_
_EST-Sile tiibrai;_
_RU-Гладкий скат;_
_FIN-Silorausku;_
_S-Slätrocka_

### Erkennungsmerkmale

![Glattrochen schematische Zeichnung](img/glattrochen/0.png)

1. Schnauze spitz (der vordere Körperrand berührt eine Linie von den Flügelspitzen zur Schnauze nicht).
2. nur eine Reihe Dornen auf dem Schwanzrücken (nicht auf dem Körperrücken; Jungtiere ohne Dornen).
3. auch zwischen den beiden Rückenflossen stehen Dornen.

* Oberseite variabel gefärbt, bräunlich mit hellen Flecken; Unterseite hellgrau.

Meist 100 cm, bis max. 150 cm Länge.

### Ähnliche Arten

* [Chagrinrochen](#chagrinrochen) - eine Reihe Dornen auf dem Nacken und zwei parallele Dornenreihen auf dem Schwanz.
* [Nagelrochen](#nagelrochen) - Schnauze stumpf; eine kräftige Dornenreihe auf Rücken und Schwanz.
* [Sternrochen](#sternrochen) - Schnauze stumpf; eine kräftige Dornenreihe auf Rücken und Schwanz.

### Lebensweise

Bodenbewohner auf Sand- und Weichböden meist bis 200 m tiefe.
Langsam wachsend, erreichen der Geschlechtsreife erst nach 11 Jahren.
Jungtiere schlüpfen nach 5 bis 10 Monaten aus Eiern.

### Ernährung

Als Jungtiere vorwiegend von bodenbewohnenden Weichtieren, als ausgewachsene Tiere hauptsächlich von Fischen.

### Bedeutung

Wirtschaftlich wichtigste Rochenart als Speisefisch in Nordwesteuropa.
In Deutschland unter dem Namen "Seeforelle" vermarktet.

### Gefährdung

Durch starke wirtschaftliche Nutzung und sehr langsamer Reproduktionsrate selten geworden.

</article>

<!-- class="sub-info" -->
> #### Dipturus batis
>
> __Familie:__ Rajidae
>
> __Ordnung:__ Rajiformes
>
> ![Karte Verbreitungsgebiet](img/glattrochen/map.png)
>
> __Verbreitung:__ Kattegat; sehr selten in der westlicher Ostsee.
>
> __Häufigkeit:__ selten
>
> __Gefährdung:__ unklar

## Atlantischer Stör

![Atlantischer Stör in Seitenansicht](img/atlantischer-stoer/1.jpg "©Vivica von Vietinghoff/DMM ")
![Atlantischer Stör - Kopf von unten](img/atlantischer-stoer/2.jpg "©Vivica von Vietinghoff/DMM")
![Atlantischer Stör in Seitenansicht](img/atlantischer-stoer/3.jpg "©Vivica von Vietinghoff/DMM")
![Atlantischer Stör - Kopf in Seitenansicht](img/atlantischer-stoer/4.jpg "©Vivica von Vietinghoff/DMM")

<article class="main-info">

_D-Atlantischer Stör;_
_GB-Atlantic sturgeon;_
_DK-Vestatlantisk stør;_
_PL-Jesiotr ostronosy;_
_LT-Aštriašnipis eršketas;_
_EST-Atlandi tuur;_
_RU-Американский атлантический осётр;_
_FIN-Sinisampi;_
_S-Atlantisk stör_

### Erkennungsmerkmale

![Atlantischer Stör schematische Zeichnung](img/atlantischer-stoer/0.png)

1. Schnauze eher lang (Strecke von der Schnauzenspitze bis zum Auge etwa gleich lang wie vom Auge bis zum Ende des Kiemendeckels).
2. zahlreiche Hautverknöcherungen (Dentikel) an der Flanke zwischen den Rücken- und Seitenschildern.

* Vier nicht-gefiederte Barteln an der Schnauzenunterseite.

Meistens 2 bis 3 m, bis max. 4,3 m Länge.

### Ähnliche Arten

* [Sibirischer Stör](#sibirischer-stör) - keine Dentikel zwischen Rücken- und Seitenschildern.
* [Waxdick](#waxdick) - Schnauze kurz.
* [Sterlet](#sterlet) - Barteln gefiedert.

### Lebensweise

Erwachsene Tiere wandern zum Laichen vom Meer flussaufwärts.
Je Saison können 800.000 bis 2.400.000 Eier über steinigem Grund abgegeben werden.
Nach 1 bis 3 Jahren wandern die Jungstöre ins Meer.
Erst nach 8 bis 30 Jahren erreichen sie die Geschlechtsreife.

### Ernährung

Weichtiere, Krebstiere, Würmer, Sandaale und Mückenlarven.

### Bedeutung

Bis Ende des 19. Jahrhunderts stark wirtschaftlich als Speisefisch und wegen des Kaviars genutzt.

### Gefährdung

Durch Flüssverschmutzung und -verbauung, Überfischung und sehr langsame Reproduktionsrate als weltweit stark gefährdet eingestuft.
In der Ostsee ausgestorben.

### Bermerkung

Für die Aquakultur wurden Stör-Hybriden (Kreuzungen von verschiedenen Arten) gezüchtet, die auch als Gefangenschaftsflüchtlinge vereinzelt in der Ostsee vorkommen.
Oft kann nur der Fachmann diese Hybriden erkennen und bestimmen.
Aktuell gibt es Wiederansiedlungsprojekte in Deutschland.

</article>

<!-- class="sub-info" -->
> #### Acipenser oxyrinchus
>
> __Familie:__ Acipenseridae
>
> __Ordnung:__ Acipenseriformes
>
> ![Karte Verbreitungsgebiet](img/atlantischer-stoer/map.png)
>
> __Verbreitung:__ Ehemals gesamte küstennahe Ostsee, seit den 1980er Jahren hier ausgestorben; Einzelnachweis 1996 bei der Insel Saareema / Estland.
>
> __Häufigkeit:__ sehr selten
>
> __Gefährdung:__ gefährdet

## Aal

![Aal - Kopf in Seitenansicht](img/aal/1.jpg "©Vivica von Vietinghoff/DMM ")
![Aal - Kopf in Seitenansicht](img/aal/2.jpg "©Vivica von Vietinghoff/DMM")
![Aal in Seitenansicht](img/aal/3.jpg "©Vivica von Vietinghoff/DMM")

<article class="main-info">

_D-Aal, Flussaal, Gelbaal, Blankaal;_
_GB-Eel, common eel, european eel;_
_DK-Ål;_
_PL-Węgorz europejski;_
_LT-Ungurys;_
_LV-Zutis;_
_EST-Angerjas;_
_RU-Речной угорь;_
_FIN-Ankerias;_
_S-Europeisk ål_

### Erkennungsmerkmale

![Aal schematische Zeichnung](img/aal/0.png)

1. Maul oberständig (der Unterkiefer überragt den Oberkiefer).
2. die Rückenflosse beginnt weit hinter dem Ende der Brustflosse.

* Kopfform variabel: zugespitzt oder breit; Färbung von hellgrau, bis dunkelgrau und gelb, Bauch heller.

Meist 30 bis 50 cm, max. bis 130 cm Länge.

### Ähnliche Arten

* [Conger](#conger) - Maul unterständig; Rückenflosse beginnt etwa da wo die Brustflosse endet.
* [Meerneunauge](#meerneunauge) - sieben äußere Kiemenöffnungen, keine Brustflossen.
* [Flussneunauge](#flussneunauge) - sieben äußere Kiemenöffnungen, keine Brustflossen.

### Lebensweise

Die laichreifen Erwachsenen wandern flussabwärts ins Meer und ziehen in die über 5.000 km entfernte Sargassosee.
Sie pflanzen sich nur einmal im Leben fort und sterben danach.
Die Larven driften mit dem Golfstrom nach Europa; die Jungaale wandern in die Flüsse und deren Mündungsbereiche und wachsen dort heran.

### Ernährung

Alle Arten von bodenlebenden Organismen, Fischlaich, Fische und Aas.

### Bedeutung

Hohe wirtschaftliche Bedeutung als Speisefisch.

### Gefährdung

Durch wirtschaftliche Nutzung, sehr langsame Reproduktionsraten und Flussverbauungen, die die Laichwanderungen stark behindern, ist der Flussaal stark gefährdet.
Der Aal kann nicht in Gefangenschaft nachgezogen werden.

</article>

<!-- class="sub-info" -->
> #### Anguilla anguillla
>
> __Familie:__ Anguillidae
>
> __Ordnung:__ Anguilliformes
>
> ![Karte Verbreitungsgebiet](img/aal/map.png)
>
> __Verbreitung:__ gesamte Ostsee mit Ausnahme der zentralen Bereiche
>
> __Häufigkeit:__ regelmäßig
>
> __Gefährdung:__ gefährdet

## Conger

![Conger - Kopf in Seitenansicht](img/conger/1.jpg "©Vivica von Vietinghoff/DMM ")
![Conger - Kopf in Seitenansicht](img/conger/2.jpg "©Vivica von Vietinghoff/DMM")
![Conger - Kopf in Seitenansicht (Nahaufnahme)](img/conger/3.jpg "©Vivica von Vietinghoff/DMM")

<article class="main-info">

_D-Conger, Meeraal;_
_GB-Conger, european conger;_
_DK-Conger;_
_PL-Conger;_
_EST-Harilik meriangerjas;_
_RU-Конгеры;_
_FIN-Meriankerias;_
_S-Havsål, conger_

### Erkennungsmerkmale

![Conger schematische Zeichnung](img/conger/0.png)

1. Maul unterständig (der Oberkiefer überragt den Unterkiefer).
2. Rückenflosse beginnt etwa am Ende der Brustflosse.

Meist 1 bis 1,5 m, bis max. 3 m Länge.

### Ähnliche Arten

* [Aal](#aal) - Maul oberständig; Rückenflosse beginnt weit hinter dem Ende der Brustflosse.
* [Meerneunauge](#meerneunauge) - sieben äußere Kiemenöffnungen, keine Brustflossen.
* [Flussneunauge](#flussneunauge) - sieben äußere Kiemenöffnungen, keine Brustflossen.

### Lebensweise

Erreichen der Geschlechtsreife mit 5 bis 15 Jahren.
Die Elterntiere sterben nach dem Laichen im offenen Meer.
Nach dem Schlüpfen 1 bis 2 jähriges Larvenstadium im Freiwasser.
Ab einer Länge von 15 cm deutliche Aalgestalt.

### Ernährung

Fische, Krebse und Tintenfische.

### Bedeutung

Kommerzielle Nutzung als Speisefisch.

### Gefährdung

Vermutlich nicht gefährdet.

</article>

<!-- class="sub-info" -->
> #### Conger conger
>
> __Familie:__ Congridae
>
> __Ordnung:__ Anguilliformes
>
> ![Karte Verbreitungsgebiet](img/conger/map.png)
>
> __Verbreitung:__ westliche Ostsee
>
> __Häufigkeit:__ selten
>
> __Gefährdung:__ unklar

## Gründling

![Gründling in Seitenansicht](img/gruendling/1.jpg "©Vivica von Vietinghoff/DMM ")
![Gründlinge in Seitenansicht](img/gruendling/2.jpg "©Vivica von Vietinghoff/DMM")
![Gründling - vorderer Köper in Seitenansicht (Nahaufnahme)](img/gruendling/3.jpg "©Vivica von Vietinghoff/DMM")

<article class="main-info">

_D-Gründling;_
_GB-Gudgeon;_
_DK-Grundling;_
_PL-Kiełb;_
_LT-Gružlys;_
_LV-Grundulis;_
_EST-Rünt;_
_RU-Обыкновенный пескарь;_
_FIN-Törö;_
_S-Sandkrypare_

### Erkennungsmerkmale

![Gründling schematische Zeichnung](img/gruendling/0.png)

1. 1 Paar lange Barteln am Hinterende des Oberkiefers.
2. Dunkler Streifen vor dem Auge zum Oberkiefer.
3. Große dunkle Flecken entlang der Seitenlinie.

* Körper sehr schlank und leicht seitlich zusammengedrückt im Querschnitt.
* Bräunliche Grundfärbung mit zahlreichen dunklen Flecken auf dem Rücken und an der Flanke; Rücken- und Schwanzflosse mit dunkler Musterung.

Meist 8 bis 15 cm, max. 20 cm Länge.

### Ähnliche Arten

* [Barbe](#barbe) - zwei Paar Barteln am Oberkiefer; längster Rückenflossenstrahl stachelartig und am Hinterrand gesägt; ohne Streifen vor dem Auge; deutlich größer werdend.

### Lebensweise

Lebt tagaktiv sehr bodenorientiert, meist in Schwärmen bevorzugt in klaren, fließenden Gewässern.
Laicht im Sommer an sandigen Uferbereichen.

### Ernährung

Kleine Bodentiere und Algen.

### Bedeutung

Trotz geringer Größe ein Speisefisch.
Häufig als Köderfisch verwendet.

### Gefährdung

Nicht gefährdet.

</article>

<!-- class="sub-info" -->
> #### Gobio gobio
>
> __Familie:__ Cyprinidae
>
> __Ordnung:__ Cypriniformes
>
> ![Karte Verbreitungsgebiet](img/gruendling/map.png)
>
> __Verbreitung:__ Selten in den südlichen und östlichen küstennahen Gebieten der Ostsee.
>
> __Häufigkeit:__ selten
>
> __Gefährdung:__ nicht gefährdet

## Grauhai

![Grauhai in Seitenansicht](img/grauhai/1.jpg "CC: NOAA")
![Grauhai in Sicht schräg von oben](img/grauhai/2.jpg "PD: NOAA")
![Grauhai in Seitenansicht schräg von oben](img/grauhai/3.jpg "PD: NOAA")

<article class="main-info">

_D-Grauhai, Sechskiemer;_
_GB-Bluntnose six-gill shark, cow shark;_
_DK-Seksgællet haj;_
_PL-Sześcioszpar szary;_
_EST-Kammhai;_
_RU-Шестижаберная акула;_
_FIN-Kidushai;_
_S-Sexbågig kamtandhaj_

### Erkennungsmerkmale

![Grauhai schematische Zeichnung](img/grauhai/0.png)

1. Nur eine Rückenflosse.
2. 6 Kiemenspalten.

* Unterer Lappen der Schwanzflosse kaum ausgebildet.
* Rücken meist dunkel gräulich oder bräunlich; Bauch heller.

Meist um 3 m, bis max. 4,8 m Länge und 590 kg Gewicht.

### Ähnliche Arten

* [Heringshai](#heringshai) - 2 Rückenflossen; nur 5 Kiemenspalten.
* [Blauhai](#blauhai) - 2 Rückenflossen; nur 5 Kiemenspalten.

### Lebensweise

Lebt bodennah meist in 100 bis 2000 m Tiefe und ist nachtaktiv.
Je Wurf werden 22 bis 108 Junge lebend geboren.

### Ernährung

Alle Arten von Boden bewohnenden Weichtieren und Fischen, auch Rochen, andere Haie, Aas und gelegentlich auch Robben.

### Bedeutung

Keine hohe wirtschaftliche Nutzung, jedoch lokale Nutzung als Speisefisch, zur Fischmehl- und Fischölgewinnung.

### Gefährdung

Häufiger Beifang in Langleinen-, Schlepp- und Stellnetzfischerei und gilt als anfällig für Überfischung, da erst sehr spät geschlechtsreif werdend:
Männchen ab etwa 3 m, Weibchen erst ab etwa 4 m Länge.

</article>

<!-- class="sub-info" -->
> #### Hexanchus griseus
>
> __Familie:__ Hexanchidae
>
> __Ordnung:__ Hexanchiformes
>
> ![Karte Verbreitungsgebiet](img/grauhai/map.png)
>
> __Verbreitung:__ Irrgast in der westlichen Ostsee.
>
> __Häufigkeit:__ sehr selten
>
> __Gefährdung:__ unklar

## Gemeiner Dornhai

![Gemeiner Dornhai in Seitenansicht](img/gemeiner-dornhai/1.jpg "©Timo Moritz/DMM")
![Gemeiner Dornhai - Kopf in Seitenansicht](img/gemeiner-dornhai/2.jpg "©Timo Moritz/DMM")
![Gemeiner Dornhai Rückenflosse (Nahaufnahme)](img/gemeiner-dornhai/3.jpg "©Timo Moritz/DMM")

<article class="main-info">

_D-Gemeiner Dornhai;_
_GB-Spurdog;_
_DK-Pighaj;_
_PL-Koleń pospolity, koleń;_
_LV-dzelkņu haizivs;_
_EST-Harilik ogahai;_
_RU-Катран;_
_FIN-Piikkihai;_
_S-Pigghaj_

### Erkennungsmerkmale

![Gemeiner Dornhai schematische Zeichnung](img/gemeiner-dornhai/0.png)

1. Dornen an beiden Rückenflossen.

* 5 Kiemenspalten, keine Afterflosse.
* Rücken gräulich bis bräunlich; gelegentlich mit hellen Flecken.

Weibchen meist 75 bis 105 cm; Männchen 60 bis 90 cm Länge.

### Ähnliche Arten

* [Heringshai](#heringshai) - ohne Dornen an der Rückenflosse; mit Afterflosse.
* [Blauhai](#blauhai) - ohne Dornen an der Rückenflosse; mit Afterflosse.

### Lebensweise

Lebt meist in großen Schulen über Weichgrund bis in 200 m Tiefe.
2 bis 11 Eier werden im Mutterleib über einen Zeitraum von 18 bis 22 Monaten ausgebrütet.

### Ernährung

Vor allem Fische, daneben auch Tintenfische und Krebstiere.

### Bedeutung

Eingelegtes Fleisch wird als "Seeaal" und die geräucherten Bauchlappen als "Schillerlocke" gehandelt.

### Gefährdung

Wegen langsamer Reproduktionsrate stark anfällig gegen Überfischung.
Die europäischen Bestände sind bereits stark überfischt.
"Dornhai"-Produkte werden mittlerweile aus ähnlichen Arten aus anderen Gebieten der Welt gewonnen.

</article>

<!-- class="sub-info" -->
> #### Squalus acanthias
>
> __Familie:__ Squalidae
>
> __Ordnung:__ Squaliformes
>
> ![Karte Verbreitungsgebiet](img/gemeiner-dornhai/map.png)
>
> __Verbreitung:__ sehr selten in der westlicher Ostsee; als Irrgast bis Rügen; Einzelnachweise sogar bis Finnland
>
> __Häufigkeit:__ selten
>
> __Gefährdung:__ gefährdet

## Fleckhai

![Fleckhai in Seitenansicht](img/fleckhai/1.jpg "©Timo Moritz/DMM")
![Fleckhai - Kopf in Seitenansicht](img/fleckhai/2.jpg "©Timo Moritz/DMM")
![Fleckhai - Kopf von unten](img/fleckhai/3.jpg "©Timo Moritz/DMM")
![Fleckhai - Seitenansicht Schwanzflosse](img/fleckhai/4.jpg "©Timo Moritz/DMM")

<article class="main-info">

_D-Fleckhai;_
_GB-Blackmouth shark;_
_DK- Ringhaj;_
_PL-Piłogon;_
_EST-Mustsuu-saagsabahai;_
_RU-Испанская акула-пилохвост;_
_FIN-Rengashai;_
_S-Hågäl_

### Erkennungsmerkmale

![Fleckhai schematische Zeichnung](img/fleckhai/0.png)

1. Charakteristische Fleckenfärbung.
2. Zweite Rückenflosse wenig kleiner als erste Rückenflosse.
3. Stark gesägter oberer Rand am Schwanzstiel.

* 5 Kiemenspalten.
* Maul-Innenseiten schwarz.

Weibchen bis 90 cm, Männchen bis 60 cm Länge

### Ähnliche Arten

* [Kleingefleckter Katzenhai](#kleingefleckter-katzenhai) - ohne Sägekante am oberen Rand des Schwanzstieles; Maulinnenseiten nicht schwarz.

### Lebensweise

Lebt meist im Tiefenwasser unterhalb von 200 m Tiefe, gelegentlich bis in nur 50 m Tiefe; eierlegend.

### Ernährung

Muscheln, Tintenfische, Krebstiere und Fische.

### Bedeutung

Keine wirtschaftliche Bedeutung.

### Gefährdung

Häufiger Beifang in Schleppnetzen und an Langleinen, aber vermutlich nicht gefährdet.

</article>

<!-- class="sub-info" -->
> #### Galeus melastomus
>
> __Familie:__ Scyliorhinidae
>
> __Ordnung:__ Carchariniformes
>
> ![Karte Verbreitungsgebiet](img/fleckhai/map.png)
>
> __Verbreitung:__ Irrgast in der westlichen Ostsee.
>
> __Häufigkeit:__ sehr selten
>
> __Gefährdung:__ nicht gefährdet

## Kleingefleckter Katzenhai

![Kleingefleckter Katzenhai in Seitenansicht](img/kleingefleckter-katzenhai/1.jpg "©Vivica von Vietinghoff/DMM")
![Kleingefleckter Katzenhai in Seitenansicht](img/kleingefleckter-katzenhai/2.jpg "©Vivica von Vietinghoff/DMM")
![Kleingefleckter Katzenhai in Seitenansicht](img/kleingefleckter-katzenhai/3.jpg "©Vivica von Vietinghoff/DMM")
![Kleingefleckter Katzenhai in Seitenansicht (Rumpf)](img/kleingefleckter-katzenhai/4.jpg "©Vivica von Vietinghoff/DMM")

<article class="main-info">

_D-Kleingefleckter Katzenhai;_
_GB-Smallspotted catshark;_
_DK-Småplettet rødhaj;_
_PL-Rekinek psi;_
_EST-Koerhai;_
_RU-Обыкновенная кошачья акула;_
_FIN-Pistepunahai;_
_S-Småfläckig rödhaj_

### Erkennungsmerkmale

![Kleingefleckter Katzenhai schematische Zeichnung](img/kleingefleckter-katzenhai/0.png)

1. Erste Rückenflosse beginnt hinter dem Ansatz der Bauchflossen.

* 5 Kiemenspalten.
* hellbraune Körperfärbung mit zahlreichen kleinen, dunklen Punkten.

Meist 75 cm, bis max. 100 cm Länge.

### Ähnliche Arten

* [Fleckhai](#fleckhai) - mit Sägekante am oberen Rand des Schwanzstieles, Maulinnenseiten schwarz.

### Lebensweise

Bodenbewohner bis max. 550 m Tiefe, meist jedoch zwischen 50 m und 250 m Tiefe, Eierlegend, 90 bis 115 pro Jahr, die ganzjährig, meist an Tangen oder Seegras, abgelegt werden.

### Ernährung

Bodenlebende Wirbellose und kleinere Fische.

### Bedeutung

Geringe Bedeutung.
In England gelegentlich als "Rock Salmon" und in Südfrankreich als "Saumonette" gehandelt.

### Gefährdung

Nicht gefährdet.

</article>

<!-- class="sub-info" -->
> #### Scyliorhinus canicula
>
> __Familie:__ Scyliorhinidae
>
> __Ordnung:__ Carchariniformes
>
> ![Karte Verbreitungsgebiet](img/kleingefleckter-katzenhai/map.png)
>
> __Verbreitung:__ Kattegat; Irrgast in der Beltsee.
>
> __Häufigkeit:__ regelmäßig
>
> __Gefährdung:__ nicht gefährdet

## Gewöhnlicher Stechrochen

![KGewöhnlicher Stechrochen](img/gewoehnlicher-stechrochen/1.jpg "PD: Florin Dumitrescu via wikimedia")
![Gewöhnlicher Stechrochen versteckt im Sand](img/gewoehnlicher-stechrochen/2.jpg "CC: Roberto Pillon via FishBase")

<article class="main-info">

_D-Gewöhnlicher Stechrochen;_
_GB-Common stingray;_
_DK-Pigrokke;_
_PL-Ogończa pastynak;_
_EST-Harilik astelrai;_
_RU-Морской кот;_
_FIN-Keihäsrausku;_
_S-Spjutrocka_

### Erkennungsmerkmale

![Gewöhnlicher Stechrochen schematische Zeichnung](img/gewoehnlicher-stechrochen/0.png)

1. Ein oder zwei Stacheln an der Schwanzbasis (kann bei manchen Individuen abgebrochen sein).

* Körperscheibe annähernd rund.

Meist 40 bis 150 cm, bis max. 200 cm Länge.

### Ähnliche Arten

### Lebensweise

Nachtaktiver Bodenbewohner auf Sand- und Weichböden bis 200 m Tiefe.
Nach einer Tragzeit von 4 Monaten werden meist 4 bis 9 Junge lebend geboren.
Es sind 2 Würfe pro Jahr möglich.

### Ernährung

Bodenbewohnende Wirbellose und Fische.

### Bedeutung

Kommerzielle Nutzung im Mittelmeer und im Schwarzem Meer.

### Gefährdung

Häufiger Beifang beim Fang von bodennahen Fischen.

</article>

<!-- class="sub-info" -->
> #### Dasyatis pastinaca
>
> __Familie:__ Dasyatidae
>
> __Ordnung:__ Myliobatiformes
>
> ![Karte Verbreitungsgebiet](img/gewoehnlicher-stechrochen/map.png)
>
> __Verbreitung:__ Westliche Ostsee
>
> __Häufigkeit:__ sehr selten
>
> __Gefährdung:__ unklar

## Nagelrochen

![Nagelrochen in Seitenansicht](img/nagelrochen/1.jpg "©Vivica von Vietinghoff/DMM")
![Nagelrochen in Seitenansicht](img/nagelrochen/2.jpg "©Vivica von Vietinghoff/DMM")
![Nagelrochen Bauchansicht](img/nagelrochen/3.jpg "©Vivica von Vietinghoff/DMM")
![Nagelrochen in Seitenansicht](img/nagelrochen/4.jpg "©Vivica von Vietinghoff/DMM")
![Nagelrochen - Kopf in Seitenansicht](img/nagelrochen/5.jpg "©Vivica von Vietinghoff/DMM")

<article class="main-info">

_D-Nagelrochen;_
_GB-Thornback ray;_
_DK-Sømrokke;_
_PL-Raja nabijana;_
_EST-Ogarai;_
_RU-Морская лисица;_
_FIN-Okarausku;_
_S-Knaggrocka_

### Erkennungsmerkmale

![Nagelrochen schematische Zeichnung](img/nagelrochen/0.png)

1. Schnauze stumpf (der vordere Körperrand läuft entlang einer Linie von den Flügelspitzen zur Schnauze).
2. eine Reihe Dornen vom Rücken auf den Schwanz laufend.
3. auffälliges Streifenmuster auf dem Schwanz.

* Weitere Dornenreihen auf dem Schwanz; die einzelnen Dornen haben eine glatte Basis.
* Oberseite hellbraun mit lebhafter Musterung (Flecken und Augenflecken).

Meist 80 bis 90 cm, bis max. 120 cm Länge.

### Ähnliche Arten

* [Sternrochen](#sternrochen) - Schwanz ohne Streifenmuster; Dornen mit geriffelter Basis.
* [Glattrochen](#glattrochen) - Schwanz ohne Streifenmuster; Schnauze spitz; nur eine Reihe Dornen auf den Schwanz begrenzt.
* [Chagrinrochen](#chagrinrochen) - Schwanz ohne Streifenmuster; eine Reihe Dornen auf dem Nacken und zwei parallele Dornenreihen auf dem Schwanz.

### Lebensweise

Vorwiegend nachtaktive Bodenbewohner bevorzugt auf Sand und Weichgrund bis 700m Tiefe.
Erreichen der Geschlechtsreife nach 9 Jahren.
Pro Jahr können 141 bis 167 Eikapseln gelegt werden.

### Ernährung

Bevorzugt von Krebstieren, jedoch auch von anderen Wirbellosen und Fischen.

### Bedeutung

Kommerziell genutzte Art in Nordwesteuropa, sowie im Mittel- und Schwarzen Meer.

### Gefährdung

Starker Rückgang der Bestände, durch langsame Reproduktionsraten und wirtschaftliche Nutzung.

</article>

<!-- class="sub-info" -->
> #### Raja clavata
>
> __Familie:__ Rajidae
>
> __Ordnung:__ Rajiformes
>
> ![Karte Verbreitungsgebiet](img/nagelrochen/map.png)
>
> __Verbreitung:__ Sehr selten in der westliche Ostsee.
>
> __Häufigkeit:__ sehr selten
>
> __Gefährdung:__ unklar

## Sternrochen

<article class="main-info">

_D-Sternrochen;_
_GB-Starry ray, thorny ray;_
_DK-Tærbe;_
_PL-Płaszczka gwiaździsta;_
_EST-Täht-sünkrai;_
_RU-Zvezdchatiy skat;_
_FIN-Kynsirausku;_
_S-Klorocka_

### Erkennungsmerkmale

![Sternrochen schematische Zeichnung](img/sternrochen/0.png)

1. Schnauze stumpf (der vordere Körperrand läuft entlang einer Linie von den Flügelspitzen zur Schnauze).
2. eine Reihe sehr großer Dornen vom Rücken bis auf den Schwanz laufend.

* Oberseite braun bis dunkelbraun ohne Musterung.

Meist bis 60 cm, max. bis 100 cm Länge.

### Ähnliche Arten

* [Nagelrochen](#nagelrochen) - gemusterte Oberseite; Schwanz mit Streifenmuster
* [Glattrochen](#glattrochen) - Schnauze spitz; nur eine Reihe Dornen auf den Schwanz begrenzt.
* [Chagrinrochen](#chagrinrochen) - eine Reihe Dornen auf dem Nacken und zwei parallele Dornenreihen auf dem Schwanz; Färbung auf der Oberseite eher grau.

### Lebensweise

Bodenbewohner auf Weich- und Felsgrund, meist zwischen 50 bis 100 m, max. bis 1000 m Tiefe; eierlegend.

### Ernährung

Vorwiegend von Krebstieren und kleineren Fischen.

### Bedeutung

Speisefisch, jedoch kaum wirtschaftliche Bedeutung.

### Gefährdung

Sinkende Bestände vor allem durch Beifang.

</article>

<!-- class="sub-info" -->
> #### Amblyraja radiata
>
> __Familie:__ Rajidae
>
> __Ordnung:__ Rajiformes
>
> ![Karte Verbreitungsgebiet](img/sternrochen/map.png)
>
> __Verbreitung:__ Kattegat; sehr selten in der westlichen Ostsee.
>
> __Häufigkeit:__ selten
>
> __Gefährdung:__ gefährdet

## Chagrinrochen

<article class="main-info">

_D-Chagrinrochen;_
_GB-Shagreenray;_
_DK-Gøgerokke;_
_PL-Raja kosmata;_
_EST-Šagrään-helerai;_
_RU-Шагреневый скат;_
_S-Näbbrocka_

### Erkennungsmerkmale

![Chagrinrochen schematische Zeichnung](img/chagrinrochen/0.png)

1. Eine Dornenreihe auf dem Rücken.
2. zwei parallele Dornenreihen auf dem Schwanz.
3. keine Dornen zwischen den beiden Rückenflossen.

* Schnauze eher spitz.
* Oberseite einheitlich grau bis dunkelgrau ohne Musterung.

Meist 30 bis 70 cm, bis max. 120 cm Länge.

### Ähnliche Arten

* [Glattrochen](#glattrochen) - nur eine Reihe Dornen auf den Schwanz begrenzt; Dornen auch zwischen den Rückenflossen.
* [Nagelrochen](#nagelrochen) - Schnauze stumpf; gemusterte Oberseite; stark ausgebildete Dornenreihe vom Rücken bis auf den Schwanz ziehend.
* [Sternrochen](#sternrochen) - Schnauze stumpf; stark ausgebildete Dornenreihe vom Rücken bis auf den Schwanz ziehend; eher braun gefärbt.

### Lebensweise

Bodenbewohner auf Hart-, Geröll- und gelegentlich Weichböden, bevorzugt kältere Wasserschichten in 30 bis 550 m Tiefe; eierlegend.

### Ernährung

Bevorzugt von Fischen, aber auch von bodenbewohnenden Wirbellosen und Krebstieren.

### Bedeutung

Keine wirtschaftliche Bedeutung, wird nur lokal befischt.

### Gefährdung

Häufiger Beifang der Schlepp- und Langleinenfischerei.

</article>

<!-- class="sub-info" -->
> #### Leucoraja fullonica
>
> __Familie:__ Rajidae
>
> __Ordnung:__ Rajiformes
>
> ![Karte Verbreitungsgebiet](img/sternrochen/map.png)
>
> __Verbreitung:__ Irrgast in der westlichen Ostsee (Einzelfund von 1890).
>
> __Häufigkeit:__ sehr selten
>
> __Gefährdung:__ gefährdet

## Lachs

![Lachs in Seitenansicht](img/lachs/1.jpg "©Vivica von Vietinghoff/DMM")
![Lachs in Seitenansicht](img/lachs/2.jpg "©Vivica von Vietinghoff/DMM")
![Lachs Jungtier in Seitenansicht](img/lachs/3.jpg "©Andi Hartl")
![Lachs - Seitenansicht Kopf](img/lachs/4.jpg "©Vivica von Vietinghoff/DMM")

<article class="main-info">

_D-Lachs;_
_GB-Atlantic salmon;_
_DK-Laks;_
_PL-Lõhe;_
_LT-Lašiša;_
_LV-Lasis;_
_EST-Lõhe;_
_RU-Атлантический лосось;_
_FIN-Lohi;_
_S-Atlantlax_

### Erkennungsmerkmale

![Lachs schematische Zeichnung](img/lachs/0.png)

1. Fettflosse vorhanden, meist nur gräulich ohne Rotanteile.
2. Maulspalte sehr groß, (meist) bis hinter das Auge reichend.
3. Schwanzstiel eher lang und schmal.

* Zahlreiche dunkle Punkte auf dem Körper (nicht auf der Schwanzflosse); Jungtiere auch mit dunklen, vertikalen Streifen.

Meist 30 bis 40 cm, bis max. 120 cm Länge.

### Ähnliche Arten

* [Meerforelle](#meerforelle) - Fettflosse oft rötlich-braun; Schwanzstiel kürzer und dicker.
* [Buckellachs](#buckellachs) - schwarze Flecken auf der Schwanzflosse.
* [Regenbogenforelle](#regenbogenforelle) - rötlich-rosa Kiemendecken und Streifen auf der Flanke.
* [Rapfen](#rapfen) - ohne Fettflosse.

### Lebensweise

1 bis 4 jährige Fress- und Wachstumsphase im Meer als Vorbereitung auf die Laichwanderung in die Flüsse.
Keine Nahrungsaufnahme während der gesamten Aufstiegs- und Laichphase.
8.000 - 25.000 Eier werden je Weibchen in Laichgruben gelegt.
Nur ein geringer Anteil der Lachse wandert zurück ins Meer, viele Tiere sterben an Überanstrengung.

### Ernährung

Kleinere Fische wie Heringe, Sandaale und Stichlinge, aber auch Krebstiere.

### Bedeutung

Sehr starke kommerzielle Nutzung als Speisefisch; häufig in Aquakultur gehalten; beliebter Angelfisch.

### Gefährdung

Steigende Gefährdung und Beeinflussung von wildlebenden Populationen durch Wasserverunreinigung, Flussverbauung (= Verhinderung der Laichwanderung) und Überfischung.

</article>

<!-- class="sub-info" -->
> #### Salmo salar
>
> __Familie:__ Salmonidae
>
> __Ordnung:__ Salmoniformes
>
> ![Karte Verbreitungsgebiet](img/lachs/map.png)
>
> __Verbreitung:__ Gesamte küstennahe Ostsee und einmündende Flüsse.
>
> __Häufigkeit:__ regelmäßig
>
> __Gefährdung:__ gefährdet

## Meerforelle

![Meerforelle in Seitenansicht](img/meerforelle/1.jpg "©Timo Moritzf/DMM")
![Meerforelle in Seitenansicht](img/meerforelle/2.jpg "©Vivica von Vietinghoff/DMM")
![Meerforelle in Seitenansicht (Kopf)](img/meerforelle/3.jpg "©Vivica von Vietinghoff/DMM")
![Meerforelle in Seitenansicht](img/meerforelle/4.jpg "©Vivica von Vietinghoff/DMM")

<article class="main-info">

_D-Meerforelle;_
_GB- Sea trout;_
_Brown trout;_
_DK-Havørred;_
_PL-Troć wędrowna;_
_LT-Šlakis;_
_LV-Taimiņš;_
_EST-Meriforell;_
_RU-Кумжа;_
_FIN-Taimen;_
_S-Öring_

### Erkennungsmerkmale

![Meerforelle schematische Zeichnung](img/meerforelle/0.png)

1. Fettflosse vorhanden und oft leicht rot-bräunlich gefärbt.
2. Maulspalte groß, meist bis unter das Auge reichend.
3. Schwanzstiel eher kurz und dick.

Meist 70 cm, max. bis 140cm Länge.

### Ähnliche Arten

* [Lachs](#lachs) - Schwanzstiel länger und dünner; Fettflosse gräulich (nicht rötlich-bräunlich)
* [Regenbogenforelle](#regenbogenforelle) - rötlich-rosa Kiemendecken und Streifen auf der Flanke.
* [Buckellachs](#buckellachs) - schwarze Flecken auf der Schwanzflosse.
* [Rapfen](#rapfen) - ohne Fettflosse.

### Lebensweise

Nach Erreichen der Laichreife mit ca. 2 Jahren wandern sie flussaufwärts.
Bis 10.000 Eier werden, ähnlich wie beim Lachs, in Laichgruben gelegt.
Die meisten Tiere überleben die Laichwanderung, kehren zurück ins Meer und können noch mehrmals zum Laichen wandern.

### Ernährung

Im Meer Fische wie Heringe, Sandaale, Stichlinge, aber auch Krebstiere; im Süßwasser vorwiegend Insektenlarven und Weichtiere.

### Bedeutung

Hoher wirtschaftlicher Wert: beliebter Speise- und Angelfisch.

### Gefährdung

Steigende Gefährdung und Beeinflussung durch Wasserverunreinigung, Flussverbauung (= Verhinderung der Laichwanderung) und Überfischung.

</article>

<!-- class="sub-info" -->
> #### Salmo trutta trutta
>
> __Familie:__ Salmonidae
>
> __Ordnung:__ Salmoniformes
>
> ![Karte Verbreitungsgebiet](img/meerforelle/map.png)
>
> __Verbreitung:__ Gesamte küstennahe Ostsee und einmündende Flüsse.
>
> __Häufigkeit:__ häufig
>
> __Gefährdung:__ unklar

## Regenbogenforelle

![Regenbogenforelle in Seitenansicht](img/regenbogenforelle/1.jpg "©Timo Moritzf/DMM")
![Regenbogenforelle in Seitenansicht (Kopf)](img/regenbogenforelle/2.jpg "©Vivica von Vietinghoff/DMM")

<article class="main-info">

_D-Regenbogenforelle;_
_GB-Rainbow trout, steelhead;_
_DK-Regnbueørred;_
_PL-Pstrąg tęczowy;_
_LT-Vaivorykštinis upėtakis;_
_LV-Varavīksnes forele;_
_EST-Vikerforell;_
_RU-Микижа;_
_FIN-Kirjolohi;_
_S-Regnbåge_

### Erkennungsmerkmale

![Regenbogenforelle schematische Zeichnung](img/regenbogenforelle/0.png)

1. Fettflosse vorhanden.
2. rötlich schillernder Kiemendeckel und Seitenband.
3. gesamter Rücken und Flanken dunkel punktiert (auch Rücken-, Fett- und Schwanzflosse); Bauch heller.

Meist 60 bis 70 cm, max. 120 cm Länge

### Ähnliche Arten

* [Buckellachs](#buckellachs) - ohne rötlich-rosa Streifen auf der Flanke.
* [Lachs](#lachs) - ohne rötlich-rosa Streifen auf der Flanke; Schwanzflosse ohne schwarze Punkte.
* [Meerforelle](#meerforelle) - ohne rötlich-rosa Streifen auf der Flanke; Schwanzflosse ohne schwarze Punkte.
* [Rapfen](#rapfen) - ohne Fettflosse.

### Lebensweise

Wildbestände mit natürlicher Fortpflanzung in Europa sehr selten; natürlich vorkommend in Nordamerika und Nordostasien.

### Ernährung

Vorwiegend Weichtiere, aber auch kleinere Fische.

### Bedeutung

Hohe wirtschaftliche Bedeutung als Speisefisch; sehr häufig in Aquakultur gehalten.

### Gefährdung

Nicht gefährdet; nicht heimisch im Ostseegebiet.

</article>

<!-- class="sub-info" -->
> #### Oncorhynchus mykiss
>
> __Familie:__ Salmonidae
>
> __Ordnung:__ Salmoniformes
>
> ![Karte Verbreitungsgebiet](img/regenbogenforelle/map.png)
>
> __Verbreitung:__ Durch Besatzmaßnahmen regelmäßig in gesamter küstennaher Ostsee und einmündenden Flüssen.
>
> __Häufigkeit:__ sehr selten
>
> __Gefährdung:__ nicht gefährdet

## Ostseeschnäpel

![Ostseeschnäpel in Seitenansicht](img/ostseeschnaepel/1.jpg "©Vivica von Vietinghoff/DMM")
![Ostseeschnäpel in Seitenansicht (nah)](img/ostseeschnaepel/2.jpg "©Vivica von Vietinghoff/DMM")
![Ostseeschnäpel in Seitenansicht](img/ostseeschnaepel/3.jpg "©Vivica von Vietinghoff/DMM")
![Ostseeschnäpel - Seitenansicht Schwanz](img/ostseeschnaepel/4.jpg "©Vivica von Vietinghoff/DMM")
![Ostseeschnäpel - Seitenansicht Kopf](img/ostseeschnaepel/5.jpg "©Vivica von Vietinghoff/DMM")

<article class="main-info">

_D-Ostseeschnäpel;_
_GB-Maraena, whitefish;_
_DK-Helt;_
_PL-Sieja;_
_EST-Merisiig;_
_RU-сея;_
_FIN-Siika;_
_S-Älvsik_

### Erkennungsmerkmale

![Ostseeschnäpel schematische Zeichnung](img/ostseeschnaepel/0.png)

1. Fettflosse.
2. "nasenförmige" Schnauze.
3. kleines, unterständiges Maul.

* Körper mit einheitlich silbrig glänzende Schuppen bedeckt.

Meist 40 bis 50 cm, max. 75cm Länge.

### Ähnliche Arten

* [Zährte](#zährte) - ohne Fettflosse; Körper deutlich höher; Afterflosse viel länger.
* [Kleine Maräne](#kleine-maräne) - Maul klein, end- bis oberständig; Schnauze nicht nasenartig verlängert.

### Lebensweise

Nach erreichen der Laichreife mit 3 bis 5 Jahren wandern die Tiere flussaufwärts und überwintern oft in den Flussarmen, wo sie dann auch laichen.
Die Jungtiere wandern auf der Futtersuche ins Meer.

### Ernährung

Zooplankton wie Krebstiere und Larven, bodenbewohnende Wirbellose, und gelegentlich kleinere Fische.

### Bedeutung

Geringe Bedeutung als Speisefisch.

### Gefährdung

Deutlich sinkende Bestände durch Wasserverunreinigung, Flussverbauung, und Überfischung.
Die Eier reagieren empfindlich auf Sauerstoffarmut (diese entsteht durch Algenblüten in überdüngten Gewässern).

### Bermerkung

Durch Besatzmaßnahmen wird versucht die Bestände in Europa zu stabilisieren.
Spezialisten unterscheiden mehrere Formen, die teils als eigene Arten angesehen werden, z.B. Coregonus widegreni, die deutlich schlanker ist und eine weniger stark ausgebildete Schnauze besitzt als C. maraena.
Schnäpel werden oft in eine eigene Familie gestellt, die Coregonidae.

</article>

<!-- class="sub-info" -->
> #### Coregonus maraena
>
> __Familie:__ Coregonidae
>
> __Ordnung:__ Salmoniformes
>
> ![Karte Verbreitungsgebiet](img/ostseeschnaepel/map.png)
>
> __Verbreitung:__ Gesamte küstennahe Ostsee und einmündende Flüsse.
>
> __Häufigkeit:__ selten
>
> __Gefährdung:__ gefährdet

## Kleine Maräne

![Zwei Kleine Maränen in Seitenansicht und Vorderansicht](img/kleine-maraene/1.jpg "©Andi Hartl")
![Kleine Maräne in Seitenansicht](img/kleine-maraene/2.jpg "©Andi Hartl")

<article class="main-info">

_D-Kleine Maräne;_
_GB-Vendace, Baltic cisco;_
_DK-Heltling;_
_PL-Sielawa;_
_LT-Seliava;_
_LV-Repsis;_
_EST-Varavīksnes forele;_
_RU-Европейская ряпушка;_
_FIN-Muikku;_
_S-Siklöja_

### Erkennungsmerkmale

![Kleine Maräne schematische Zeichnung](img/kleine-maraene/0.png)

1. Fettflosse vorhanden.
2. Maul klein und end- bis leicht oberständig.

* silbrig glänzend, Flanken meist blau-grün gefärbt.

Meist 15 bis 20 cm, max. 40 cm Länge.

### Ähnliche Arten

* [Ostseeschnäpel](#ostseeschnäpel) - nasenartige Schnauze.
* [Ukelei](#ukelei) - ohne Fettflosse; Afterflosse viel länger (länger als Rückenflosse).
* [Hering](#hering) - ohne Fettflosse; Maul größer und stärker oberständig.
* [Stint](#stint) - Maul deutlich größer; Seitenlinie unvollständig.

### Lebensweise

Sowohl Süß-, als auch Salzwasser-bewohnende Arten; oft auch Migrationen von Salz- in Süßwasser aus Fortpflanzungsgründen; erreichen der Laichreife mit 2 bis 5 Jahren.

### Ernährung

Vor allem kleines Zooplankton wie Krebstiere und deren Larven.

### Bedeutung

Wirtschaftliche Nutzung als Speisefisch.

### Gefährdung

Vermutlich nicht gefährdet.

</article>

<!-- class="sub-info" -->
> #### Coregonus albula
>
> __Familie:__ Coregonidae
>
> __Ordnung:__ Salmoniformes
>
> ![Karte Verbreitungsgebiet](img/kleine-maraene/map.png)
>
> __Verbreitung:__ Im Golf von Finnland und Bottnischen Meerbusen; küstennah und einmündende Flüsse.
>
> __Häufigkeit:__ regelmäßig
>
> __Gefährdung:__ unklar

## Stint

![Stint in Seitenansicht](img/stint/1.jpg "©Timo Moritz/DMM")
![Stint in Seitenansicht (nah)](img/stint/2.jpg "©Timo Moritz/DMM")

<article class="main-info">

### Erkennungsmerkmale

![Stint schematische Zeichnung](img/stint/0.png)

1. Fettflosse
2. lange Maulspalte, reicht bis unter das Auge.

* schlanker Körper mit relativ großen Schuppen (im Vergleich mit Lachsen und Forellen).
* charakteristischer 'gurkenartiger' Geruch.
* nie mit Flecken auf den Flossen.
* Seitenlinie unvollständig.

Meist 8 bis 16 cm, max. 30 cm Länge.

### Ähnliche Arten

* [Kleine Maräne](#kleine-maräne) - Maul deutlich kleiner; Seitenlinie vollständig.

### Lebensweise

Küstennaher Schwarmfisch in 12 bis 30 m Tiefe; nach ereichen der Laichzeit, mit 1 bis 2 Jahren, wandern sie flussaufwärts; Weibchen legen 8.000 bis 50.000 Eier über sandigem oder kiesigem Grund.
Viele Tiere sterben nach dem Laichen.

### Ernährung

Zooplankton; meist Krebstiere, deren Larven und verschiedene andere Larven, selten auch Jungfische.

### Bedeutung

Wirtschaftliche Bedeutung als Speisefisch, zur Öl- und Futtermittelherstellung.

### Gefährdung

Generell vermutlich nicht gefährdet; jedoch sind viele lokal begrenzte Populationen durch Verbauung und Verschmutzung der Gewässer bedroht.

</article>

<!-- class="sub-info" -->
> #### Osmerus eperlanus
>
> __Familie:__ Osmeridae
>
> __Ordnung:__ Osmeriformes
>
> ![Karte Verbreitungsgebiet](img/stint/map.png)
>
> __Verbreitung:__ Gesamte küstennahe Ostsee und einmündende Flüsse.
>
> __Häufigkeit:__ sehr häufig
>
> __Gefährdung:__ nicht gefährdet

## Buckellachs

![Buckellachs in Seitenansicht im Fluss liegend](img/buckellachs/1.jpg "©Andi Hartl")
![Buckellachs - Kopf in Seitenansicht (nah)](img/buckellachs/2.jpg "©Andi Hartl")
![Buckellachs - auf dem Rücken liegend](img/buckellachs/3.jpg "©Andi Hartl")

<article class="main-info">

_D-Buckellachs;_
_GB-Pink salmon;_
_DK-Pukkellaks;_
_PL-Gorbusza;_
_EST-Gorbuuša;_
_RU-Горбуша;_
_FIN-Kyttyrälohi;_
_S-Puckellax_

### Erkennungsmerkmale

![Buckellachs schematische Zeichnung](img/buckellachs/0.png)

1. Fettflosse vorhanden.
2. Männchen während der Laichzeit mit ausgeprägtem Buckel.

* Schwarze Flecken auf der Schwanzflosse.
* Flanken silbern bis grau, braun oder grün, aber ohne rötliches Band.

Meist 50 cm, max. 76 cm Länge

### Ähnliche Arten

* [Regenbogenforelle](#regenbogenforelle) - rötlich-rosa Kiemendecken und Streifen auf der Flanke.
* [Lachs](#lachs) - Schwanzflosse ohne schwarze Flecken.
* [Meerforelle](#meerforelle) - Schwanzflosse ohne schwarze Flecken.

### Lebensweise

Nach erreichen der Geschlechtsreife mit 2 Jahren, wandern die Tiere flussaufwärts.
Die Weibchen bauen 1 bis 4 Nester auf dem Grund, in die jeweils 50 bis 1200 Eier gelegt werden.
Männchen und Weibchen bewachen die Nester.
Nach dem Laichen sterben alle Tiere.

### Ernährung

Fisch, Weich- und Krebstiere.

### Bedeutung

Sehr hohe wirtschaftliche Bedeutung als Speisefisch, in Aquakultur und als Angelfisch.

### Gefährdung

Nicht heimisch in der Ostsee.

</article>

<!-- class="sub-info" -->
> #### Oncorhynchus gorbuscha
>
> __Familie:__ Salmonidae
>
> __Ordnung:__ Salmoniformes
>
> ![Karte Verbreitungsgebiet](img/buckellachs/map.png)
>
> __Verbreitung:__ Sehr selten, nur durch Besatzmaßnahmen.
>
> __Häufigkeit:__ sehr selten
>
> __Gefährdung:__ nicht gefährdet

## Mondfisch

![Mondfisch in Seitenansicht](img/mondfisch/1.jpg "© Timo Moritz/DMM")
![Mondfisch in Seitenansicht](img/mondfisch/2.jpg "© Timo Moritz/DMM")
![Mondfisch in Seitenansicht](img/mondfisch/3.jpg "© Timo Moritz/DMM")

<article class="main-info">

_D-Mondfisch;_
_GB-Ocean sunfish;_
_DK-Klumpfisk;_
_PL-Samogłów;_
_LT-Paprastoji mėnulžuvė;_
_LV-Kuukala;_
_EST-Kuukala;_
_RU-Обыкновенная луна-рыба;_
_FIN-Möhkäkala;_
_S-Klumpfisk_

### Erkennungsmerkmale

![Mondfisch schematische Zeichnung](img/mondfisch/0.png)

1. Rücken- und Afterflosse lang ausgezogen.
2. Echte Schwanzflosse fehlend.

* Bauchflossen fehlend.
* seitlich abgeflachter, scheibenförmiger Körper.

Bis max. 3 m Länge und bis über 2000 kg Gewicht.

### Ähnliche Arten

Unverwechselbar

### Lebensweise

Lebt im Freiwasser tieferer Meeresbereiche, kann zuweilen aber auch seitlich an der Wasseroberfläche liegend beobachtet werden.
Es können bis zu 300 Millionen Eier abgegeben werden.

### Ernährung

Quallen, Larven von Quallen, Aalen und Kopffüßlern, sowie seltener kleine Fische.

### Bedeutung

Keine wirtschaftliche Bedeutung.

### Gefährdung

Vermutlich nicht gefährdet.

</article>

<!-- class="sub-info" -->
> #### Mola mola
>
> __Familie:__ Molidae
>
> __Ordnung:__ Tetraodontiformes
>
> ![Karte Verbreitungsgebiet](img/mondfisch/map.png)
>
> __Verbreitung:__ sehr seltener Irrgast in der Ostsee
>
> __Häufigkeit:__ sehr selten
>
> __Gefährdung:__ nicht gefährdet

## Schwarzer Seeteufel

<article class="main-info">

_D-Schwarzer Seeteufel;_
_GB-Black angler, blackbellied angler;_
_DK- Sort havtaske;_
_PL-Żabnica afrykańska;_
_EST- Mustkõht-merikurat;_
_RU- Чернобрюхий удильщик;_
_FIN- Mustavatsakrotti;_
_S- Mindre marulk_

### Erkennungsmerkmale

![Gründling schematische Zeichnung](img/schwarzer-seeteufel/0.png)

1. Kopf sehr groß und breit.
2. Maul sehr groß, halbkreisförmig.
3. Erster Rückenflossenstrahl zu einer Angel umgebildet.

* Körper abgeflacht; ohne Schuppen.
* 9 bis 10 Strahlen in der 2. Rückenflosse; schwarzes Bauchfell in der Leibeshöhle

Meistens 50 cm, max. 1 m Länge.

### Ähnliche Arten

* [Gemeiner Seeteufel](#gemeiner-seeteufel) - meist deutlich größer; 11 bis 12 Strahlen in der zweiten Rückenflosse; Bauchfell (innen) weiß.

### Lebensweise

Bodenfische auf Sand- und Schlammboden, oft auch teilweise eingegraben.
Vorkommen bis in 1000 m Tiefe.

### Ernährung

Vor allem Fische, die mit seiner Angel angelockt werden.

### Bedeutung

Wirtschaftliche Bedeutung als beliebter und teurer Speisefisch.

### Gefährdung

Vermutlich stark gefährdet durch Überfischung.

</article>

<!-- class="sub-info" -->
> #### Lophius budegassa
>
> __Familie:__ Lophiidae
>
> __Ordnung:__ Lophiiformes
>
> ![Karte Verbreitungsgebiet](img/schwarzer-seeteufel/map.png)
>
> __Verbreitung:__ Seltener Irrgast in der westlichen Ostsee.
>
> __Häufigkeit:__ sehr selten
>
> __Gefährdung:__ stark gefährdet





## OER finden
Einleitungstext

Material-Darstellung 
Gallery?
<!-- style="display: block; margin: auto; width: 60%;" -->

![Das ist ein Test](https://www.youtube.com/watch?v=65aGlJZPypY "ob das so funktioniert wie es soll")



![](Dummy_300x300px.png)

  ![Bild 1](![](Dummy_300x300px.png)![Bild 2](![](Dummy_300x300px.png) ![Bild 3](![](Dummy_300x300px.png) ![Bild 4](![](Dummy_300x300px.png) ![Bild 5](![](Dummy_300x300px.png)


Accordion?

## OER herstellen
abc

Video einbetten:
a) Placeholder with link to Youtube

[![Entwicklungsumgebung mit Groovy/Git testen](https://img.youtube.com/vi/fbZOii_l7M4/maxresdefault.jpg)](https://youtu.be/fbZOii_l7M4)

b) AV-Portal player embedded

<iframe width="560" height="315" scrolling="no" src="//av.tib.eu/player/40456" frameborder="0" allowfullscreen="allowfullscreen"></iframe>

c) Youtube embedded

<iframe width="420" height="315"
src="https://www.youtube.com/embed/fbZOii_l7M4" allowfullscreen="allowfullscreen">
</iframe>
## Mit OER lernen
abc

## Mit OER lehren
abc

## OER einführen
abc

## OER managen
abc

## OER herstellen
abc 

## über OER forschen
abc

# Impressum
This template for OER courses is released under MIT. The content of the document is subject to the respective license as indicated at the end of the generated files or in the metadata.yml.

# Impressum

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
