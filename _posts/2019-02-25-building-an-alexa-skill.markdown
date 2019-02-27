---
layout: post
title:  "Alexa Skill mit ASK und AWS Lambda"
date:   2019-02-25 10:02:50 +0100
tags:   [alexa, aws, serverless, python]
---

## Voraussetzungen

- Amazon Account
- Amazon Echo Device
- AWS account

## Skill in ASK Konsole erstellen

Die [ASK Development Console] öffnen \(Anmeldung mit Amazon-Login) und "Create Skill" klicken. Den Namen für den Skill eingeben, in unserem Fall "Mein cooler Skill". Die Optionen "Custom" und "Self Hosted" anwählen und "Create Skill" klicken 

![screenie](/assets/img/blog/create-skill-de.png)

Das führt uns zur Entwickleransicht unseres Skills. Hier im Menü links "Invocation" anwählen und unter "Skill Invocation Name" die Wörter eingeben, mit denen wir unseren Skill sprachlich aktivieren wollen. In unserem Fall ist das "meinen coolen skill", weil wir den Skill später mit "Alexa, öffne meinen coolen Skill" aktivieren wollen. Anschließend speichern wir mit "Save Model" und tun dies künftig nach jeder Änderung. 

![screenie](/assets/img/blog/set-invocation-name-de.png)

Jetzt definieren wir die Sprachäußerungen, die unser Skill nach seiner Aktivierung verstehen können soll. Dazu im Menü links bei Intents auf "+ Add" klicken und unter "Create custom intent" einen internen Namen eingeben und auf "Create Custom Intent" klicken. In unserem Fall ist der Name "SaySomethingNiceIntent", denn wir wollen, dass unser Skill uns etwas schönes, erheiterndes sagt. 

![screenie](/assets/img/blog/create-intent-de.png) 

Anschließend können wir die Sprachäußerungen eingeben, die unser Skill verstehen können soll. Unser Skill soll etwas schönes sagen und uns erheitern, indem er einfach ein zufällig gewähltes Wort aus einer Liste schöner deutscher Wörter verliest. Die entsprechenden Sprachkommandos geben wir wie folgt an. Abschließend sollten wir mit "Save Model" die Änderungen speichern.

![screenie](/assets/img/blog/create-utterances-de.png)

## Backend-Service mit AWS Lambda erstellen

Jetzt erstellen wir einen Backend-Service, der die von unserem Skill aufgezeichneten Sprachäußerungen entgegennimmt und die Antworten generiert. Dazu lassen wir den Tab mit der ASK Console geöffnet und loggen uns in einem neuen Tab bei unserer [AWS-Konsole] ein. Dort suchen wir nach "Lambda" und wechseln dann zur Lambda Management Console. Falls "Lambda" nicht gefunden werden kann, muss ggf. oben rechts eine andere Region gewählt werden (bei mir EU Ireland).  

![screenie](/assets/img/blog/open-lambda-console.png)

In der Lambda Console klicken wir auf "Funktion erstellen", wählen dann die Option "Ohne Vorgabe", wählen einen Namen ("mein_cooler_skill", Name ist nicht wichtig für Funktion) und die Laufzeit-Umgebung "Python 3.7" (oder eben die höchste akt. verfügbare Version).

![screenie](/assets/img/blog/create-lambda.png)

![screenie](/assets/img/blog/create-lambda-2.png)

Für unsere Funktion müssen wir noch eine Rolle definieren, für die wir noch spezielle Berechtigungen festlegen könnten. In unserem Fall reicht es, eine neue Rolle mit Standard-Berechtigungen zu definieren. 

![screenie](/assets/img/blog/create-role.png)

Wir nennen die neue Rolle "alexa" und bestätigen mit "Erlauben". 

![screenie](/assets/img/blog/create-role-2.png)

Zurück bei AWS Lambda wählen wir die neue Rolle aus und legen mit "Funktion erstellen" unsere Funktion an. 

![screenie](/assets/img/blog/create-lambda-3.png)

In der Entwickler-Ansicht unserer neuen Funktion scrollen wir nach unten und ersetzen den Code im Editor mit dem [Code aus meinem Repository]. Anschließend speichern wir die Datei im Editor

![screenie](/assets/img/blog/insert-lambda-code.png)



## Backend-Service mit Skill verknüpfen

In der Lambda Console kopieren wir den ARN unserer Lambda Funktion(oben rechts), wechseln zum noch geöffneten Tab mit der ASK Console unseres Skills, wählen links "Endpoint" an, selektieren den Endpoint-Typ "AWS Lambda ARN", fügen den Lamda ARN in das Feld "Default Region" ein und klicken "Save Endpoint". 

![screenie](/assets/img/blog/connect-lambda-with-skill.png)

![screenie](/assets/img/blog/connect-lambda-with-skill-2.png)

Dann kopieren wir in der ASK Console die ID unseres Skills (Feld oberhalb der Lambda ARN), wechseln zum noch geöffneten Tab mit der Lambda Console, fügen links einen Auslöser "Alexa Skills Kit" hinzu, tragen unten unter Qualifikations-ID die kopierte Skill-ID ein, klicken dann auf "Hinzufügen" und oben auf "Speichern".

![screenie](/assets/img/blog/connect-lambda-with-skill-3.png)

![screenie](/assets/img/blog/connect-lambda-with-skill-4.png)

![screenie](/assets/img/blog/connect-lambda-with-skill-5.png)

## Skill testen

Jetzt können wir unseren neuen Skill online testen. In der ASK Console wechseln wir vom Tab "Build" zum Tab "Test", wo wir zum Test unseres Skills einen Dialog mit Alexa führen können. 

![screenie](/assets/img/blog/test-skill.png)

## Skill auf unserem Amazon Echo Gerät einspielen

Wir wechseln in der ASK Console in den Tab "Distribution". Unter "Skill Preview" > "German" geben wir an:
- einen öffentlichen Namen
- eine Kurzbeschreibung ()
- eine detaillierte Beschreibung 
- die Beispielsätze, die unser Skill versteht
- großes und kleines Skill-Icon, hier das [Icon aus meinem Repository] auf den Desktop und dann in beide Felder ziehen
- eine Kategorie (Education & Reference)

Anschließend klicken wir auf "Save and continue".

![screenie](/assets/img/blog/distribute-skill.png)

![screenie](/assets/img/blog/distribute-skill-2.png)

![screenie](/assets/img/blog/distribute-skill-3.png)

Unter "Skill Preview" > "Privacy & Compliance" füllen wir das Formular wie folgt aus und bestätigen dann mit "Save and continue".

![screenie](/assets/img/blog/distribute-skill-4.png)

Unter "Skill Preview" > "Availability" wählen wir "Public". Dann wählen wir "Beta Test", um unseren Skill einfach privat auf unserem Echo testen zu können. Unter "Beta Test Administrator" tragen wir unsere E-Mail-Adresse ein und bestätigen mit "Add".
Dann setzen wir unter "Manage Access to your Skill Beta Test" das Häkchen für "EMAIL ADDRESS", tragen unter "Enter tester email addresses" ebenfalls unsere E-Mail-Adresse ein, bestätigen wieder mit "Add" und clicken anschließend auf "Enable Beta Testing".

![screenie](/assets/img/blog/distribute-skill-5.png)

![screenie](/assets/img/blog/distribute-skill-6.png)

![screenie](/assets/img/blog/distribute-skill-7.png)

Als Tester haben wir jetzt eine E-Mail erhalten und folgen dem ersten Link in der Mail, um unseren Skill auf unserem Echo zu aktivieren. 

![screenie](/assets/img/blog/distribute-skill-8.png)

Bei "Amazon Alexa" melden wir uns mit unserem Standard-Amazon-Account an. Hier werden wir entweder gleich mit einer Nachricht zur Test-Teilnahme begrüßt, oder finden "Mein cooler Skill" unter "Skills" > "Ihre Skills" > "Entwicklerskills" und können den Skill so auf unserem Gerät aktivieren.

![screenie](/assets/img/blog/distribute-skill-9.png)

![screenie](/assets/img/blog/distribute-skill-10.png)

Jetzt können wir zu unserem Echo gehen und den Dialog starten. "Alexa, öffne meinen coolen Skill und sag was schönes".
Viel Spaß!


[ASK Development Console]: https://developer.amazon.com/alexa/console/ask
[AWS-Konsole]: https://console.aws.amazon.com
[Code aus meinem Repository]: https://github.com/bahnson/my-first-alexa-skill/blob/master/lambda_function.py
[Icon aus meinem Repository]: https://github.com/bahnson/my-first-alexa-skill/blob/master/skill-icon.png
[How to Program a Conversation with Alexa! (Python & AWS Lambda) - Part 1]: https://www.youtube.com/watch?v=sj7NqS7yytw