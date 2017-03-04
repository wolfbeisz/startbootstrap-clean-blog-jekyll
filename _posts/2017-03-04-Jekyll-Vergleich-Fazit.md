---
layout: post
title: Vergleich von Jekyll und WordPress
---
# Vergleich von Jekyll und Wordpress

Anwendungsfall Blog

Jekyll | WordPress
------ | ---------
statisch und performant | dynamisch, dafür langsamer. Um diesen Nachteil auszugleichen, werden zusätzliches Features bereitgestellt, die aber die Komplexität des Gesamtsystems vergrößern (z.B. Caches).
volle Kontrolle über statische Inhalte | eingeschränkte Kontrolle über statische Inhalte
keine dynamischen Inhalte, aber Einbettung von IFrames möglich, z.B. um Kommentare bei einem anderen Dienst zu speichern | hohe Kontrolle über dynamische Inhalte (z.B. kann für die Kommentarfunktion konfiguriert werden, welche Voraussetzungen ein Besucher erfüllen muss, um kommentieren zu können. Es kann eingestellt werden, dass die Angabe einer E-Mail-Adresse ausreicht oder dass sich der Besucher registrieren muss.)
Als Entwickler gibt man Kontrolle ab, um die Webseite dynamisch zu machen. Man kann den Dienst Disqus nutzen, um eine Kommentarfunktion bereitzustellen, oder Videos von Youtube einbinden. Dadurch ist man vom Dienstanbieter abhängig; falls der Dienst eingestellt würde und die eigenen Daten nicht exportiert werden können, verliert man ggf. Daten unwiederbringlich. | Bei WordPress hat man die volle Kontrolle über die Kommentare, man wird aber auch mit den unangenehmen Seiten konfrontiert (z.B. Spam, Freischaltung von Kommentaren)
Der Betrieb der Webseite erfordert ausschließlich einen Webserver. Dieser muss regelmäßig aktualisiert werden. | Für den Betrieb von WordPress wird ein AMP-Stack verwendet (Apache, MySql und PHP). Folglich müssen drei Komponenten abgesichert und administriert werden.
Skalierbarkeit: Ein Webserver, der ein Set von statischen HTML-Dateien ausliefert kann einfacher skalieren. Man betreibt mehrere Server mit der gleichen Konfiguration und leitet die Anfrage mittels eines Load Balancers an die verschiedenen Server weiter. | Die Skalierung einer WordPress-Seite ist komplizierter, weil der Zustand zwischen den verschiedenen Servern abgeglichen werden muss. Das betrifft einerseits die Datenbanken,  die repliziert werden müssen. Andererseits müssen die Benutzer-Sessions allen WordPress-Servern bekannt sein.
Statische Webseiten enthalten per se keine Sicherheitslücken, die zum Angriff auf den Server ausgenutzt werden können. | WordPress hatte in der Vergangenheit immer wieder unterschiedlichste Arten Sicherheitslücken, die sogar dazu genutzt werden konnten, um Zugriff auf das Backend zu erlangen. Daneben können Sicherheitslücken in PHP existieren.
einfache Administration | Umfangreiche Administrationsaufgaben: Installieren von Sicherheits-Updates für WordPress; Versions-Upgrades; Anpassung eigener Themes, wenn auf eine höhere Version upgegradet wird, da sich die Anforderungen an die Theme-Definition ändern können; Prüfung der Plugin-Kompatibilität (Plugins können mit neueren Versionen inkompatibel sein, wenn der Entwickler sie nicht anpasst)
Blog-Posts bzw. Seiten werden in einem Texteditor erstellt. Es kann ein lokaler Webserver gestartet werden, der die Seite ausliefert und bei Änderung neu generiert. | WordPress hat ein webbasiertes Backend, in dem berechtigte Benutzer die Inhalte der Seite verwalten können. Neue Inhalte können mittels eines WYSIWYG-Editors erstellt werden.
Die Seiten (Pages) sind nicht hierarchisch strukturiert, sondern bilden eine flache Struktur. Deshalb kann muss man Zusatzaufwände betreiben, wenn man eine hierarchische Navigationsstruktur möchte. | In WordPress können Seiten in eine Navigationshierarchie eingefügt werden und diese Hierarchie wieder geändert werden.
Um die Seiteninhalte zu versionieren, kann man git einsetzen, da alle Informationen in Textdateien gespeichert werden. | Wordpress hat ein integriertes Feature zu Versionierung von Seiten: Jede Änderung an einer Seite / Post erzeugt eine neue Version. Ältere Versionen können angesehen und wiederhergestellt werden.

# Fazit
Ob man Jekyll oder Wordpress einsetzt, hängt von den Benutzern des Systems ab. Wenn man Jekyll einsetzt, müssen die Benutzer die Eingabeaufforderung benutzen und sich ggf. auch mit HTML und CSS beschäftigen. Wenn die Benutzer dieses Wissen nicht haben, sollte  man besser WordPress oder ein anderes CMS mit webbasierter Oberfläche einsetzen.