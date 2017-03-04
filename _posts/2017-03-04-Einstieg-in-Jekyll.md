---
layout: post
title: Einstieg in Jekyll
---
# Überblick

Jekyll ist ein Generator für statische Websites. Die grundlegende Funktionalität besteht darin, Markup-Dateien (Text-Dateien, die den syntaktischen Regeln einer Markup-Language folgen, z.B. Markdown) in HTML-Dateien zu transformieren / umzuwandeln. Bei der Transformation wird ein Layout angewendet, damit die erzeugte Seite ein einheitliches Aussehen hat. 

Die erzeugte Seite kann von einem einfachen Webserver ausgeliefert werden, d.h. genügt, die erzeugten Dateien auf Webspace hochzuladen, um sie öffentlich verfügbar zu machen. Alternativ kann man auch selbst einen Webserver betreiben und mit diesem die Dateien ausliefern.

Zusätzlich ist Jekyll so konzipiert, dass es mit relativ geringem Aufwand möglich ist, einen Blog zu erzeugen. Der Benutzer speichert jeden Blog-Beitrag in einer Markup-Datei, startet Jekyll und generiert so eine Webseite die die Blog-Einträge sowie eine Übersicht über alle Einträge enthält.

Jekyll ist auf die Generierung von Blogs ausgelegt.

Jekyll ist in Ruby implementiert. Jekyll verwendet existierende Softwarekomponenten um die beschriebenen Funktionen zu realisieren. Die Abbildung zeigt die eingesetzten Komponenten und ihre Beziehung zueinander.

Die Markup-Dateien werden vom Benutzer erzeugt und enthalten den Inhalt der Seite (z.B. Blog-Posts, Kontakt-Seite, Impressum). Jekyll erkennt anhand der Dateiendung, welche Markup-Sprache in der Datei enthalten ist (z.B. Markdown). Dann übergibt Jekyll die Datei an eine Komponente, die die Markup-Sprache in HTML umwandeln kann (hier Konverter genannt). Für die Umwandlung von Markdown in HTML wird standardmäßig kramdown verwendet. Das erzeugte HTML wird an eine Template Engine übergeben. Die Template Engine generiert aus einem Template (auch Theme genannt) zusammen mit dem übergebenen HTML eine HTML-Seite (static site). Die erzeugte HTML-Seite besteht aus Elementen aus dem Template (z.B. Navigationsleiste, Footer) und dem Inhalt aus dem ürsprünglichen Markup-File. Dieser Prozess wird für alle relevanten Markup-Dateien wiederholt.

![Jekyll-Architecture]({{ site.baseurl }}/binary/jekyll-architecture.svg)

Einzelne Elemente der Abbildung können ausgetauscht werden. Z.B. kann kramdown durch einen anderen Konverter ersetzt werden, der ebenfalls markdown in HTML umwandelt. Es könnte sein, dass ein Anwender der Konverter ersetzt, weil der Konverter zusätzliche Features hat. kramdown hat Features, die über den Markdown-Standard hinausgehen.

# Installation

Um Jekyll zu nutzen, muss eine Ausführungumbgebung für Ruby-Code verfügbar sein. Für Windows gibt es den [RubyInstaller](http://rubyinstaller.org/downloads/). Bei der Installation sollte beachtet werden, dass die Checkbox "add ruby to PATH" gesetzt wird. Anderenfalls muss der Pfad zum Installationsverzeichnis zur Umgebungsvariable PATH manuell hinzugefügt werden. Danach muss das Ruby Devkit installiert werden. Es kann [hier](https://dl.bintray.com/oneclick/rubyinstaller/DevKit-mingw64-32-4.7.2-20130224-1151-sfx.exe) für Windows heruntergeladen werden. Wenn man die Datei ausführt, wird das DevKit in ein Verzeichnis entpackt. 

Im folgenden Schritt installiert man das DevKit: Dazu öffnet man die Eingabeaufforderung und wechselt in das Verzeichnis in das das DevKit entpackt wurde. Dort führt man die folgenden Befehle aus:

```bash
ruby dk.rb init
ruby dk.rb install
```

Nach der Installation des DevKits kann Jekyll installiert werden. Jekyll ist ein Ruby-Gem und kann mithilfe des gem-Tools installiert werden:

```bash
gem install jekyll
gem install bundler
```

Die Befehle laden Jekyll und ein Tool namens Bundler aus dem Internet herunter und installieren sie. Bundler ist ein Dependency-Management-Tool für Ruby Gems. Jekyll verwendet es, um sicherzustellen, dass vor dem Start von Jekyll die erforderlichen Themes, Plugins oder Jekyll selbst in der korrekten Version auf dem System installiert sind.
Auf Systemen, auf denen mittels eines Proxies auf das Internet zugegriffen wird, kann die Installation der Gems fehlschlagen. Dann sollte man man den Proxy mittels des Parameters -p spezifizieren. Beispiel: Der Proxy ist unter der IP 10.0.0.20 auf Port 8080 verfügbar. Dann können die gems mittels
```bash
gem sources --add https://rubygems.org -p http://10.0.0.20:8080
gem install bundler -p http://10.0.0.20:8080
gem install jekyll -p http://10.0.0.20:8080
```
installiert werden.

Jetzt ist Jekyll einsatzbereit.