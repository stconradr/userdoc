---
title: URN
weight: 90
---

# URN Parameter

## Automatische URN-Generierung

Es gibt die Möglichkeit, automatisch URNs in OPUS4 zu vergeben. Das Generieren und Speichern der URN erfolgt während des Freischaltungsprozesses des Dokuments.
Im ausgelieferten `$BASEDIR/application/configs/config.ini.template` sind die entsprechenden URN-Parameter mit Testwerten befüllt
und die Funktion ist deaktiviert (`urn.autoCreate = 0`). Um die Funktion zu benutzen, müssen die Werte der Parameter
`urn.nid` und `urn.nss` Instanz-spezifisch befüllt und der Parameter `urn.autoCreate = 1` gesetzt werden.

{% highlight ini %}
; URN SETTINGS
; If you want to set URNs automatically, set urn.autoCreate to 1.
urn.autoCreate = 0             # muss zur Aktivierung auf 1 gesetzt werden
urn.nid = nbn                  # Namensraum (i.d.R. nbn)
urn.nss = de:kobv:test-opus    # de:[Bibliotheksverbund]:[Bibliothekssigel] oder de:[vierstellige Ziffer]
{% endhighlight %}

<p class="warning" markdown="1">
Die DNB lässt nur URNs für Dokumente mit Volltexten zu. Daher ist die Vergabe von URNs auf Dokumente im Status
"published" beschränkt, die per OAI sichtbare Dateien besitzen. Sichtbar per OAI sind alle Dateien, bei denen das
Attribut `VisibleInOai` auf `1` gesetzt ist.
</p>

Um zu prüfen, ob in einer früheren OPUS-Version URNs für Dokumente ohne sichtbaren Dateien vergeben wurden, kann
folgendes Script genutzt werden:

{% highlight bash %}
$ opus4/scripts/
$ php opus-console.php snippets/find_urns_for_docs_without_visible_files.php
{% endhighlight %}

Bitte achten Sie beim Migrieren von Dokumenten, die bereits URNs besitzen, darauf, innerhalb des Konfigschlüssels
`urn.nss` das Suffix, welches das digitale Objekt an sich kennzeichnet (Namespace Specific String), ggf. anzupassen. Für
das obige Beispiel könnte aus -opus z.B. -opus4 werden.

## Manuelle URN-Generierung

Sollten Sie bereits vor dem Freischalten des Dokuments eine URN benötigen, um z.B. die URN im Volltext einzufügen, kann diese manuell auf den Seiten der DNB generiert werden (siehe [NBN-Prüfziffer-Berechnung][URN-Berechnung]).

Unter Angabe des URN-Namensraum und der OPUS-ID wird die Prüfsumme der URN berechnet. Die generierte URN kann dann in OPUS über die Administration im Feld "Identifier - URN" eingetragen werden.

{% highlight bash %}
z.B.
die OPUS-ID:  urn:nbn:de:kobv:test-opus-5838
ergibt folgende URN: urn:nbn:de:kobv:test-opus-58386
{% endhighlight %}


[URN-Berechnung]: http://nbn-resolving.de/nbnpruefziffer.php

* [URN-Vergabe](../introduction.html#urn-vergabe)
{: class="navlist" }
