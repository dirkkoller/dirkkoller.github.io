---
layout: article
title: "Postprocessing mit RTKLIB"
image:
  teaser: gps-referenzpunkt.jpg
  feature:
---

Im Beitrag <DGPS mit RTKLIB> wurde gezeigt wie sich mit einem Raw-Empfänger und RTKLIB zentimetergenaue Positionen messen lassen. Die Korrektur der Daten mit Hilfe von SAPOS erfolgte dabei über das Internet in Echtzeit mittels NTRIP. Das ist praktisch weil man warten kann, bis die Position fix und damit gut bestimmt ist. Unglücklicherweise gibt es aber auch Orte oder Situationen in denen die Daten nicht "life" bezogen werden können (GPS-Messungen in Funklöchern oder ein RTK-GPS auf einer Drohne ohne Internetempfang). Hier bietet sich as Alternative zu aufwendigeren Workflows (wie eine Funkverbindung zwischen Basis und Rover) die nachträgliche Korrektur der Positionen an. Das Verfahren nennt sich Postprocessing oder genauer Post-Processed Kinematic (PPK) und soll in diesem Beitrag erläutert werden.
	
Auch für das Postprocessing-Verfahren werden RAW-Daten mit Trägerphasen und Pseudodistanzen benötigt. Ein Empfänger der diese Daten bei entsprechender Konfiguration liefern kann ist zum Beispiel der u-blox M8T.

# Erfassung der Raw-Daten

Die Erfassung der Raw-Daten geschieht hier mit Hilfe des Programms u-center. 

Config: reach_single_default.conf
Positioning Mode:	Single
nput source for base corrections:	Off
Raw data log for onboard receiver: file

Man erhält mit diesen Einstellungen eine ubx-Datei im herstellerspezifischen Binärformat. Darin sind alle benötigten Informationen enthalten. Die Datei kann im u-Center geladen und abgespielt werden. 

# Rinex-Konvertierung mit rtkconf

Das so erhaltene File wird mit rtkconf, einer Anwendung aus dem rtklib-Pogrammpaket nach RINEX konvertiert. RINEX steht für "Receiver Independent Exchange Format", ist also ein herstellerunabhängiger Standard. Die Rinex-Version kann unter Optionen ausgewählt werden. Start- und Endzeit brauchen nicht eingegeben zu werden.

Zusätzlich zu den so erhaltenen Rinex-Daten des Rovers werden die Daten einer Basisstaion benötigt. SAPOS bietet diese wahlweise von festen Basisstationen oder virtuellen an. Vor dem Download wird die Uhrzeit und Dauer der Messung in GPS-Zeit abgefragt.


# Postprocessing mit RTKPost

Nun kann das Porstprocessing mit RTKPost beginnen.

Positioning Mode: Static (für unbewegtes Messung)
Base Station: Rinex Header Position
Output Format:	NMEA
Rinex observerd Rover
Rinex observerd Base
Rinex nav (wurde von Base genommen)





