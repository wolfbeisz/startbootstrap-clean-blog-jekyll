---
layout: post
title: Jekylls Features
---
# Grundlegende Features

Um eine neue Seite zur erstellen führt man 
```bash
jekyll new <pfad-zu-verzeichnis>
```

aus. Jekyll erstellt das angegebene Verzeichnis und erzeugt das Grundgerüst für eine Jekyll Seite. Das Grundgerüst besteht aus Dateien und Verzeichnissen. Diese definieren die Inhalte der Seite und deren Aussehen (Layout). 

## Verzeichnisstruktur

Die Verzeichnisstruktur einer neu erzeugten Jekyll-Seite entspricht unter Windows folgender Struktur.
```
25.02.2017  11:13    <DIR>          .
25.02.2017  11:13    <DIR>          ..
25.02.2017  11:12                35 .gitignore
25.02.2017  11:12               525 about.md
25.02.2017  11:12               981 Gemfile
25.02.2017  11:13             1.321 Gemfile.lock
25.02.2017  11:12               213 index.md
25.02.2017  11:12             1.402 _config.yml
25.02.2017  11:12    <DIR>          _posts
               6 Datei(en),          4.477 Bytes
               3 Verzeichnis(se), 27.891.191.808 Bytes frei
```

Das Verzeichnis `_posts` enthält die Blog-Posts, die veröffentlicht werden sollen. Posts müssen einer Dateinamenskonvention folgen: Der Dateiname setzt sich zusammen aus dem Datum der Veröffentlichung im Format YYYY-MM-DD, dem Titel, in dem Whitespace-Characters durch Minus (-) ersetzt werden und der Dateiendung. Die beiden Teile werden ebenfalls durch Minus voneinander getrennt. 
Ein Post (geschrieben in Markdown) mit dem Titel "Hello World", veröffentlicht am 02.01.2017, wird in einer Datei mit dem Namen "2017-01-02-Hello-World.md" gespeichert.

Im Verzeichnis befinden sich zwei Dateien, die durch die Endung `*.md` als Markdown-Dateien gekennzeichnet sind (index.md und about.md). Die beiden Dateien wurden von Jekyll generiert und demonstrieren die Markdown-Syntax. Beide Dateien sind sogenannte Pages. Pages sind inhaltlich wie Posts aufgebaut, unterscheiden sich aber darin, dass sie an einer beliebigen Stelle im Jekyll-Projekt abgelegt werden dürfen und keine "Gruppe" bilden. Posts bilden eine Gruppe, da sie mit einem Datum versehen sind und deshalb chronologisch sortiert werden können.

Die Datei `_config.yml` enthält Jekylls globale Konfiguration. Einerseits werden in der Datei globale Variablen - die von der Template-Engine ausgewerter werden können - definiert, andererseits können darin Standardwerte für die Parameter der Jekyll-Kommandozeilenapplikation festgelegt werden. Ebenfalls darin wird definiert, welches Template verwendet werden soll.

Als Daumenregel lässt sich sagen, dass jedes Verzeichnis bzw. jede Datei, deren Name mit einem Unterstrich beginnt, eine besondere Bedeutung für Jekyll hat.

Wenn man mit Jekyll eine Webseite generiert (siehe "Generieren einer Seite"), werden die erzeugten Dateien in das Verzeichnis `_site` kopiert. `_site` ist auf der gleichen Verzeichnisebene wie `_posts` und die anderen oben aufgelisteten Dateien.

Weitere wichtige Verzeichnisse, die bisher nicht erwähnt wurden, und nicht notwendigerweise benötigt werden sind `_drafts`, `_layouts` und `_includes`.
* Drafts sind unveröffentlichte Posts; ihr Dateiname beginnt nicht mit einem Zeitstempel. Drafts sind in der generierten Seite nicht enthalten. 
* Layouts enthält HTML-Templates (Vorlagen), die die Template-Engine mit Inhalten füllt. Die Vorlage wrappt den Inhalt, d.h. es werden Elemente um den Inhalt herum eingefügt (z.B. Navigationleiste, Header, Footer). Wenn man ein eigenes Template entwickelt, speichert man die Vorlagen in diesem Verzeichnis.
* Includes sind wiederverwendbare Seitenbestandteile (HTML), die in Pages / Posts / Drafts eingebunden werden können, z.B. der HTML-Code zum Einbetten eines Youtube-Videos.

## Generieren der Seite
Um die Webseite zu generieren, so dass sie z.B. auf den eigenen Webserver übertragen werden kann, führt man
```
bundler exec jekyll build
```
aus. Wenn dieser Befehl ausgeführt wird, generiert Jekyll aus den Posts bzw. Pages HTML-Seiten (entsprechend des oben abgebildeten Prozesses) und kopiert diese HTML-Seiten in das Verzeichnis `_site`. Posts, Pages, Drafts und andere Dateien werden unterschiedlich behandelt:
* Posts werden in HTML-Seiten transformiert und in einer Verzeichnishierarchie abgelegt, die das Datum wiederspiegelt. Ein Post, der am 02.01.2017 verfasst wurde ("2017-01-02-Hello-World.md") findet sich als HTML-Datei als `_site/2017/01/02\Hello-World.html` wieder. Es werden nur Posts generiert, deren zugeordnetes Datum nicht in der Zukunft liegt.
* Pages (z.B. index.md, about.md) werden ebenfalls in HTML-Dateien umgewandelt. Sie werden in der gleichen Verzeichnis-Hierarchie abgelegt, in der sie sich im Jekyll-Projekt-Verzeichnis befinden. `index.md` wird nach `_site/index.md` kopiert. TODO: Abgrenzung zwischen verschiedenen Dateitypen (*.css wird nicht in html umgewandelt, markdown schon)
* Drafts werden standardmäßig nicht generiert. Wenn der Parameter `--drafts` gesetzt wird, werden sie Pages behandelt.
* Statische Dateien (z.B. eine gedachte index.html) werden von Jekyll in das entsprechende Unterverzeichnis in `_site` kopiert.

Vor dem Generieren werden alle Inhalte des Verzeichnisses `_site` gelöscht.
wertet Jekyll die globale Konfiguration (_config.yml) aus.


## Starten eines lokalen Webservers

Um die Seite zu generieren und einen Webserver zu starten, wechselt man in das zuvor angegebene Verzeichnis und führt
```
bundler exec jekyll serve --no-watch
```
aus. Wenn man der URL folgt, die auf der Konsole ausgegeben wird (standardmäßig http://127.0.0.1:4000/), sieht man auf im Browser folgende Seite.

![Jekyll Minima Theme]({{ site.baseurl }}/binary/minima-screenshot.png)

## Exkurs: YAML
YAML ist eine vereinfachte Auszeichnungssprache zur menschenlesbaren Darstellung von Datenstrukturen. Mit YAML können assoziative Listen (Dictionaries), Listen (Arrays) und Skalare (einzelne Werte) repräsentiert werden. [1](https://de.wikipedia.org/wiki/YAML)
Listen von Werten werden wie Aufzählungen repräsentiert:
```yaml
- alpha
- beta
- gamma
```

Assoziative Listen werden Folge von Zeilen repräsentiert, wobei der Key (Schlüssel) und der Value (Wert) eines Elements durch einen Doppelpunkt getrennt werden.
```yaml
name: John Doe
geburtstag: 01.01.1970
```

Für Listen als auch assoziative Listen gibt es eine Inline-Syntax. Eine Liste kann als `[element1, element2, element3]` geschrieben werden. Eine assoziative Liste kann als `{key: value}` repräsentiert werden.

## Erstellen eines Posts

Einen neuen Post verfasst man, indem man eine neue Textdatei erstellt, deren Name der oben beschriebenen Konvention entspricht, und sie im Verzeichnis `_posts` speichert. Als Zeichenkodierung sollte UTF-8 ohne BOM (Byte Order Mark) verwendet werden. 
Das folgende Listing zeigt beispielhaft den Inhalt eines Posts. Dieser besteht aus einem Front-Matter (eine Art Header, der Jekyll anweist, die Datei zu verarbeiten). Der Front-Matter wird eingeleitet durch  `---` und endet mit eben dieser Zeichenfolge. Dazwischen befindet sich YAML-Markup. 

Der YAML-Markup weist Jekyll an, das Layout mit dem Namen `post` zu verwenden. Beim Generieren der Seite lädt die Template Engine die Datei `post.html` und ersetzt den Platzhalter für den Inhalt durch das HTML, das der Konverter aus dem Post generiert hat. 
Außerdem wird die Variable `title` gesetzt. Die Variable wird in vielen Templates verwendet, um dem HTML-Element `<title>` einen sinnvollen Wert zuzuweisen.

Auf das Front-Matter folgt der Inhalt des Posts. Für den Inhalt des Posts wird in den meisten Fällen Markdown verwendet. Es ist jedoch auch möglich, HTML zu verwenden. Github Guides bietet eine verständliche, mit Beispielen versehene [Einführung in Markdown](https://guides.github.com/features/mastering-markdown/#examples).

```markdown
---
layout: post
title: Der Titel eines Posts
---
kramdown-style toc
* Inhaltsverzeichnis
{:toc}

# Überschrift 1 (wie h1)

Hier folgt der Text des Blog-Posts.

Eine Aufzählung (ul)
* alpha
* beta
* gamma
* delta

Eine nummerierte Liste (ol)
1. Look up
2. Get up
3. And don't ever give up

Zitat:
> Look up. Get up. And don't ever give up

## Unterüberschrift (wie h2)

# Top-Level Überschrift
Setzen von [Links](http://www.google.de/) und Einbinden eines Bildes ![Logo](https://www.google.de/images/branding/googlelogo/1x/googlelogo_color_272x92dp.png) ist einfach.

Textabschnitte können *kursiv* oder **fett** formatiert werden.
```

Innerhalb des Front-Matters können folgende Variablen gesetzt werden:
* date: Datum und Uhrzeit des Posts (YYYY-MM-DD HH:MM:SS +/-TTTT)
* categories: Liste von Kategorien, in die ein Post fällt
* tags: Liste von zugeordneten Schlagworten

### Variablen im Front-Matter
Zusätzlich dazu können eigene Variablen definiert werden und danach verwendet werden. Die Ersetzung der Variablenausdrücke im Content-Bereich führt die Template-Engine durch. Beispiel:
```markdown
---
layout: post
title: Variablen mit Liquid
meine_variable: wert1
---
{% raw %}{{ page.meine_variable }}{% endraw %}
```

In dem Post würde der Ausdruck `{% raw %}{{ page.meine_variable }}{% endraw %}` durch den Wert der Variablen `meine_variable` ersetzt werden (hier: "wert1"). Templates funktioneren prinzipiell nicht anders: Sie setzen einen HTML-Header vor den Inhalt und schließen alle geöffneten Tags. Um auf Variablen zuzugreifen, die in dem Post definiert wurden, wird `page.` dem Variablennamen vorangestellt. Um auf Variablen zuzugreifen, die in `_config.yml` definiert wurden, wird `site.` den Variablen vorangestellt. Die Abbildung stellt den Zusammenhang zwischen Front-Matter, `_config.yml` und den verfügbaren Variablen graphisch dar:

![Variable Flow]({{ site.baseurl }}/binary/jekyll-process-post.svg)


## Erstellen einer Page
Eine Page wird genauso erstellt wie ein Blog-Post, mit dem Unterschied, dass sich die Datei an einer selbst gewählten Stelle im Jekyll-Projekt-Verzeichnis befinden darf. Das bedeutet, dass eigene Verzeichnisse und Unterverzeichnisse im Jekyll-Projekt-Verzeichnis erstellt werden dürfen und Markup-Files darin abgespeichert werden dürfen. Beim Generieren bleibt die selbst definiert Verzeichnisstruktur erhalten: Die Verzeichnisstruktur wird unterhalb des Ausgabeverzeichnisses `_site` übernommen.
Der Dateiname ist nicht den gleichen Einschränkungen unterworfen wie bei Posts: Es muss nur sichergestellt werden, dass die Dateiendung mit der verwendeten Markup-Sprache übereinstimmt (z.B. *.md für Markdown bzw. *.html für HTML).

Inhaltlich ist eine Page wie ein Post aufgebaut: Zuerst der Header (`---`, Front-Matter und wieder `---`), dann der Inhalt in einer Markup-Sprache. Beispiel:
```markdown
---
layout: page
title: demo
---
# This file shows how a page is created

Your text here.
```

Hier wurde page als Layout definiert. Im Vergleich zum Layout post verzichtet page auf die Darstellung von Informationen, die nur für Blog-Posts verfügbar sind (z.B. Veröffentlichungsdatum oder Autor). page ist keine Konstante in dem Sinn, dass `page` immer ein gültiger Wert wäre. Für die meisten Templates existiert jedoch ein gleichnamiges Layout. Falls ein Layout nicht existiert, wird beim Generieren der Seite ein Hinweis ausgegeben.

## Anpassen der Konfiguration (_config.yml)
Jekylls globale Konfiguration wird in `_config.yml` als assoziative Liste gespeichert (siehe: Exkurs YAML). Die Themes können auf die Elemente der Liste zugreifen; sie sind im Namensraum `site` verfügbar. Seitenbezogenene Informationen wie Name der Seite, Kurzbeschreibung oder E-Mail, die in allen generierten HTML-Seiten vorhanden sein sollen, können hier definiert werden. Genau das macht das `minima`-Theme:
```yaml
title: Your awesome title
email: your-email@domain.com
description: > # this means to ignore newlines until "baseurl:"
  Write an awesome description for your new site here. You can edit this
  line in _config.yml. It will appear in your document head meta (for
  Google search results) and in your feed.xml site description.
```

Als Seitenentwickler ersetzt man die Platzhalter durch die gewünschten Werte (z.B. `Your awesome title` durch `Mein Blog`) und generiert die Seite neu.

## Wechsel des Themes

In Jekyll existieren zwei Möglichkeiten, Themes zu verwalten: Der ältere Ansatz ist, die Layouts und alle zusätzlich benötigten Dateien (z.B. CSS-Dateien, Javascript-Dateien, Icons) im Jekyll-Projekt-Verzeichnis abzuspeichern. Die Layouts werden im Verzeichnis `_layouts` gespeichert, andere Dateien dürfen an beliebigen Orten im Jekyll-Projekt gespeichert werden und werden von Jekyll beim Generieren in das Ausgabeverzeichnis `_site` kopiert.

Der neuere Ansatz ist, die Themes in eigene Gems auszulagern. Die Layouts und Assets werden in einem eigenen Gem zusammengefasst. Innerhalb des Gems wird die gleiche Verzeichnisstruktur verwendet wie innerhalb eine Jekyll-Projekts. D.h. innerhalb des Gems gibt es ein `_layouts`-Verzeichnis usw. Die Dateien innerhalb des Gems werden so behandelt als befänden sie sich innerhalb des Jekyll-Projekts. Existiert eine Datei mit dem gleichen relativen Pfad sowohl im Gem als auch im Jekyll-Projekt, so verwendet Jekyll die Datei aus dem Projekt-Verzeichnis. So kann man ein Gem-basiertes Theme verwenden und trotzdem eigene Änderungen daran vornehmen.
Der Vorteil der Gem-basierten Themes ist, dass sie leichter ausgetauscht werden können, da das Jekyll-Projekt mit den Blog-Posts und Pages vom Layout getrennt wird (anderer Speicherort). Leider ist die Auswahl Gem-basierter Themes noch beschränkt, da es für den Entwickler eines Layouts zusätzlichen Aufwand bedeutet.

### Ersetzen des Standard-Themes durch ein anderes Gem-basiertes Theme
Das Standard-Theme heißt [Minima](https://github.com/jekyll/minima). Im Folgenden wird beschrieben, wie man zu dem Gem-basierten Theme [Athena](https://github.com/broccolini/athena) wechselt. Dafür sind drei Schritte erforderlich:
1. Bearbeiten des `Gemfile`: Im Gemfile werden die Abhängigkeiten des Jekyll-Projekts definiert. Die Zeile  `gem "minima", "~> 2.0"` wird durch `gem "jekyll-athena", "0.0.2"` ersetzt. `jekyll-athena` ist der Name des Ruby-Gems, das das Athena-Theme enthält. Der Gem-Name wird vom Theme-Entwickler festgelegt; er ist in der URL des Ruby-Gems erkennbar: `https://rubygems.org/gems/jekyll-athena`
2. Ausführen von `bundle install` in der Eingabeaufforderung
3. Bearbeiten der `_config.yml`: In der Datei wird festgelegt, welches Theme verwendet werden soll. Die Zeile `theme: minima` wird durch `theme: jekyll-athena` ersetzt.
4. Generieren der Seite / Starten des lokalen Webservers: Die Seite der muss neu generiert werden, damit die Änderungen wirksam werden. Bzw. der lokale Webserver muss neu gestartet werden (`bundle exec jekyll serve`), weil die `_config.yml` nur einmal eingelesen wird.

Bei Planet Jekyll ist eine [Liste](https://github.com/planetjekyll/awesome-jekyll-themes#official-themes) mit Gem-basierten Jekyll-Themes verfügbar.

### Classic Themes

Neben den Gem-basierten Themes gibt es viele "classic" Themes, die die Layouts im Jekyll-Projekt ablegen. Um eines der klassischen Themes zu verwenden, lädt man das Theme herunter und kopiert dann eigene Inhalte in die entsprechenden Verzeichnisse (z.B. `_posts` oder eigene Pages). Danach führt man `bundle exec jekyll serve` aus und überprüft, ob die Seite generiert werden kann. Ist das der Fall, sollte man ebenfalls überprüfen, ob die Inhalte korrekt dargestellt werden.

Es gibt deutlich mehr classic als Gem-basierte Themes. Kostenlose Themes werden auf folgenden Webseites bereitgestellt:
* [https://jekyllthemes.io](https://jekyllthemes.io)
* [https://github.com/andrewbanchich](https://github.com/andrewbanchich)