# Mediamatiker Modul 286

# Aufträge am 27.01.2020

## Angestrebte Kompetenzen und Lernziele

- Ich kenne die Bedeutung des CHANGELOG
- Ich kann ein CHANGELOG für mein Projekt führen
- Ich kann recherche im Repository durchführen

## Umgang mit `git log`

Der Zweck eines jeden Versionskontrollsystems besteht darin, Änderungen an unserem Code festzuhalten.
Aber all die Historie verfügbar zu haben, bringt uns nichts, solange wir nicht wissen, wie wir in ihr navigieren.
An dieser Stelle kommt der Befehl `git log` ins Spiel.

```bash
git log                      # Zeigt die gesamte Commit-Historie in der voreingestellten Formatierung an.
git log readme.txt           # Commits, die readme.txt verändert haben.
git log -n 3                 # Zeigt die Commit-Historie der letzten 3 Commits.
git log --since="3 days ago" # Zeigt die Commit-Historie der letzten 3 Tage.
git log --oneline            # Komprimiert jeden Commit auf eine einzelne Zeile.
git log --oneline --decorate # Die Option --decorate weist Git an, alle Referenzen (also Branches, Tags usw.) anzuzeigen, die auf jeden Commit verweisen.
git log --author="<muster>"  # Sucht nach Commits eines bestimmten Autoren.
git log --grep="<muster>"    # Sucht nach Commits mit Commit-Beschreibung, die auf <muster> passen.
```

Die interessanteste Option ist format, mit der Sie Ihr eigenes Log-Ausgabeformat festlegen können. 
Dieses Verfahren ist besonders nützlich: da Sie das Format explizit angeben, wissen Sie, dass es sich mit Updates von Git nicht ändert:
Nützliche Optionen für `git log --pretty=format` listet einige der nützlichsten Optionen auf, die `format` bietet.

```bash
git log --pretty=format:'%an commited "%s" (%h) %ar'
git log --format="  * %s"
# When you create a commit that should be listed in the changelog just place #changelog in the commit message (probably on the second line so it doesn't show). 
git log v0.1.1...v0.1.2 --pretty=format:'- [view commit](http://github.com/<username>/<project>/commit/%H) &bull; %s ' --reverse | grep "#changelog"
```

**Tip: Die Anzeige von Merge-Commits unterdrücken**
Fügen Sie einfach die Log-Option `--no-merges` hinzu.

## Aufgaben

- Lassen Sie sich alle Commits der letzten Stunde ausgeben.
- Lassen Sie sich alle Commits ausgeben, die die Datei README.md verändert haben.
- Erstellen Sie ein CHANGELOG für die bisherigen Änderungen. (Leistungsnachweis / 3 Punkte)

## Weiterführende Links und Quellen

- [Git Grundlagen - Anzeigen der Commit-Historie](https://git-scm.com/book/de/v2/Git-Grundlagen-Anzeigen-der-Commit-Historie)
- [Führe ein CHANGELOG](https://keepachangelog.com/de/1.0.0/)
- [Recherche im Repository](https://www.ralfebert.de/git/log-recherche/)
- [gitchangelog generates a changelog thanks to git log.](https://pypi.org/project/gitchangelog/)

## Aufträge am 20.01.2020

- Pendenzen vom 6.1.2020 aufarbeiten! Es fehlt immer noch eine **Bibliothek für icons bzw. glyphs**.

### Leistungsnachweis (Bewertung am 27.01.2020)

- `develop` branch erstellt (1P)
- `crazy` branch erstellt und mindstens 3 (leere) Dateien hinzugefügt  (1P)
- `master` branch mit tag v0.1.0  (1P)

### Erstellung von Enwicklungszweigen (Branches, Merge) und Versionen (Tags)

Die **Versionsnummer** ist die Grundlage für die Versionsverwaltung. Den Prozess der Vergabe der Versionsnummer nennt man Versionierung. Für die Software-Entwicklung stellen Versionsnummern eine weitaus wichtigere Information als für den Kunden dar. Mit Hilfe der Versionsnummern kann unter anderem sichergestellt werden, dass in Entwicklergruppen neue Programmteile nicht mit älteren überschrieben werden.

Auf Grundlage einer Versionsnummer von `MAJOR.MINOR.PATCH` nach der [Semantic Versioning Spezifikation](https://semver.org/lang/de/) werden die einzelnen Elemente folgendermassen erhöht:

1. MAJOR wird erhöht, wenn (API-)inkompatible Änderungen veröffentlicht werden,
2. MINOR wird erhöht, wenn neue Funktionalitäten, welche kompatibel zur bisherigen API sind, veröffentlicht werden, und
3. PATCH wird erhöht, wenn die Änderungen ausschliesslich API-kompatible Bugfixes umfassen.

**Tags** werden verwendet, um wichtige Punkte in der Projekthistorie zu markieren. Tags können anstelle der Commit-Hashes verwendet werden, um Commits zu referenzieren. *Es ist üblich, bei einem Release den jeweiligen Commit mit einer Versionsnummern (Tag) zu versehen.* Git unterstützt sog. *Annotierte Tags*, diese werden als vollständige Objekte in der Git-Datenbank gespeichert. Somit enthalten Sie den Author, die E-Mail und das Datum, haben eine Meldung und können mit GNU Privacy Guard (GPG) signiert und überprüft werden.

Ein **Branch** repräsentiert eine **unabhängige Entwicklungslinie**. Wenn wir ein neues Feature hinzufügen oder einen Bug fixen wollen – unabhängig von der Grösse –, setzen wir einen neuen Branch auf, um unsere Änderungen abzukapseln. So wird sichergestellt, dass instabiler Code nicht direkt ins Hauptprojekt committet wird, und wir haben die Möglichkeit, die History unseres Features aufzuräumen, bevor wir es in den Haupt-Branch mergen.

#### Übung: `git tag`

**Reproduzieren Sie die folgende Anweisungen in ihrem persönlichem Repository.**

Die folgende Anweisung erzeugt ein neuer kommentierten Tag, das mit v1.4 identifiziert wird:

```bash
git tag -a v1.4 -m "my version 1.4"
```

Um die gespeicherte Tags in einem Repo aufzulisten, führen wir folgender Befehl aus:

```bash
git tag
```

Standardmässig beinhaltet ein `git push` keine Tags. Diese müssen explizit an `git push` übergeben werden.

```bash
git push origin v1.4
```

#### Übung: `git branch`

**Reproduzieren Sie die folgende Anweisungen in ihrem persönlichem Repository.**

Erstellen wir einen Branch mit dem folgenden Befehl:

```bash
git branch crazy-experiment
```

Auf diese Weise wird lediglich ein neuer Branch erstellt. Wenn wir beginnen wollen, ihm Commits hinzuzufügen, müssen wir ihn mit `git checkout` auswählen und dann die Standardbefehle `git add` und `git commit` verwenden.

```bash
git checkout crazy-experiment // Checkt den spezifischen Branch aus, der mit `git branch` erstellt wurde.
```

Um einen Branch zu erstellen und diesen direkt einzusetzen, führen wir folgende Anweisung durch:

```bash
git checkout -b fancy-experiment
```

Und zu letzt:

```bash
git branch // Listet alle Branches im Repository auf.
```

Ändern Sie nun einige Dateien und fügen Sie neue dazu. Speichern Sie Ihre Arbeit mit `git add`, `git commit`, `git tag` und `git push`.

Kehren Sie danach zurück in den `master` Branch. **Was stellen Sie fest?**

#### Aufgabe: `git merge`

Finden Sie heraus wie Sie Änderungen aus dem Branch `fancy-experiment` in den `master` Branch übernehmen können.

Nachdem wir die Änderungen zusammengeführt haben, können wir meist den Branch löschen. Dabei bleiben die Hauptverzweigungen `master` und `develop` erhalten.

### Weiterführende Links

- [Git Grundlagen - Tagging](https://git-scm.com/book/de/v2/Git-Grundlagen-Tagging)
- [Git: Mit Branches arbeiten (git checkout)](https://blog.seibert-media.net/blog/2015/08/04/git-mit-branches-arbeiten-git-checkout/)
- [Git Branching](https://git-scm.com/book/de/v2/Git-Branching-Einfaches-Branching-und-Merging)
- [Git Branching - Branches auf einen Blick](https://git-scm.com/book/de/v2/Git-Branching-Branches-auf-einen-Blick)
- [A successful Git branching model](https://nvie.com/posts/a-successful-git-branching-model/)

## Aufträge am 13.01.2020

- [Der HTML-Editor ist ein unverzichtbares Werkzeug, deshalb wähle weise](https://www.drweb.de/8-besten-kostenlosen-html-editoren-webentwickler-windows-edition-53187/)
- [Kostenlose HTML-Editoren: Die 11 Besten für Webentwickler unter macOS](https://www.drweb.de/5-besten-kostenlosen-html-editoren-webentwickler-mac-edition-53159/)

### Leistungsnachweis (Bewertung am 20.01.2020)

In dieser Aufgabe sollen Sie grundlegende handwerkliche Schritte durchführen, die bei der Webentwicklung ständig benötigen werden. Vieles von dem, was Sie für diese Aufgabe anwenden, benötigen Sie auch in anderen Bereichen ausserhalb der Webentwicklung.

#### "Offizielles" Repository anlegen (3P)

Zunächst richten Sie sich ein Repository ein, das zur zentralen Ablage Ihrer Arbeitsergebnisse dient. Auf ein solches zentrales Repository können Sie sowohl von einem Laborrechner als auch von ihren privaten Geräten zugreifen, und dabei Ihre Arbeit synchron halten. Lesen Sie bei Bedarf in der [offiziellen Git-Dokumentation](https://git-scm.com/book/de/v2) (insbesondere Abschnitte 2.1 und 2.2, evtl. auch 2.5) nach.

- Legen Sie ein neues Git-Repository für diese Aufgabe an.
- Fügen Sie die Dozenten (Account: `visialog` `foxfabi`) als "Berechtigten Nutzer" hinzu.
- Klonen Sie Ihr frisch angelegtes Git-Repository auf Ihren Arbeitsrechner.

#### "Hallo Welt" erstellen (3P)
Im zweiten Schritt geht es darum, eine erste Datei zu erstellen, und so die Basis für alles weitere zu legen. Natürlich beginnen wir mit einem "Hallo, Welt!".

- Erstellen Sie eine Datei mit dem Inhalt `Hallo, Welt!`; speichern Sie sie als `index.html` im Wurzelverzeichnis der Arbeitskopie Ihres Git-Klons.
- Öffnen Sie diese Datei in Ihrem Webbrowser.
- Wenn Sie zufrieden sind, erstellen Sie einen Git-Commit, der diese Datei beinhält. Wählen Sie dabei eine aussagekräftige Commit-Message.
- Pushen Sie diesen Commit in Ihr Repository.

## Aufgabe: Website Skeleton

- HTML / CSS Framework evaluieren und einbinden
- jQuery einbinden und script erstellen (Light/Dark Mode)
- Wichtige Ressourcen aus README in Webseite portieren


## Aufgabe: Client installieren

**Brauche ich eigentlich den GitHub-Desktop-Client, um mit GitHub zu arbeiten?**

Mit GitHub kann man auf verschiedenen Wegen arbeiten.
Über die Kommandozeile nimmt man das Programm git, das bei macOS und Linux meist vorinstalliert ist;
Windows-Nutzer finden den Download weiter unten. Der Desktop-Client erleichtert das Klonen,
Committen und Pushen von Repositories in einer grafischen Oberfläche.
Wer ausser GitHub noch andere Git-Hoster nutzt, dem empfehlen wir einen Blick auf grafische
Git-Clients wie Tower, GitKraken und SourceTree. Aus vielen Programmierumgebungen kann man per
Erweiterung auch direkt einen Commit in Git-Projekten erzeugen.

## Summary:

### Git Lokal:

 - git init --> Erstellt neues repository
 - git add --> Fügt Files hinzu
 - git commit -m "changes on the readme" --> Änderung bestätigen und Nachricht dazu schreiben
 - git status --> liefert Informationen über die Datein der eigenen Arbeitskopie
 - git diff --> Aktuellen Dateiinhalt mit dem Stand des letzten Commits vergleichen

 ### GitHub:

 - git init --> Erstellt neues repository
 - clone --> repository clonen (= kopieren)
 - fork --> Abzweigung des ursprünglichen repositorys
 - pull request --> eigene Version vom repository zum Antrag stellen
 - merge --> Eigene bearbeitete Version zum orginalen repository hinzufügen
 - sync --> Synchronisation zwischen Lokaler Datenbank und Remote Datenbank


## Werkzeuge / Tool:

* [**Git for Windows**](https://git-scm.com/download/win) / [**Git for Mac**](https://git-scm.com/download/mac)
* [**Tortoise Git: The Power of Git – in a Windows Shell**](https://tortoisegit.org/)
* [**GitHub Desktop**](https://desktop.github.com/)
* Alle Tools als Übersicht  https://git-scm.com/book/de/v2

## Vorgehensweise / Prozess

## Nützliche Links und Quellen
* [Wissenswertes über github](https://t3n.de/news/eigentlich-github-472886/)
* [Was ist github](https://kinsta.com/de/wissensdatenbank/was-ist-github/)
* [Repository anlegen und code hochladen](https://legacy.thomas-leister.de/github-fuer-anfaenger-repository-anlegen-und-code-hochladen/)
* [Unterschied zwischen Github, Gitlab (englisch)](https://usersnap.com/blog/gitlab-github/)

## Markdown Syntax
![Markdown Syntax] (https://markdown.de)


![Übersicht Wandtafel](./assets/images/wandtafel_zusammenfassung_git_github.jpeg)
