In diesem Bereich finden sich verschiedene Code-Snippets. ALLE (!) Snippets sind **work-in-progress** und noch nicht fertiggestellt - sie sollen nur dem Einstieg in diese Bereiche der Trovis-Visualisierung in Home Assistant dienen. Hilfe ist gern willkommen!

# **Die Originalvorlage**
Diese komplett interaktive Ansicht habe ich ca. 2014 begonnen - seit 2019 ist sie fast unverändert, es werden im Minutentakt Daten gelogged und visualisiert. Das Backend ist SmartHomeNG, das Frontend die smartVISU. Ziel meines HA-Projektes ist, diese Anzeige so originalgetreu wie möglich in HA zu implementieren (mit einigen verbesserungen).

Hier ein Screenshot aus der Heizperiode:
![__Vorlage - smartVISU im Einsatz__](https://github.com/user-attachments/assets/dd0faec7-c7be-47ee-b9c6-371eeabb3a05)

# Datei ha-visu_aktuell.yaml

Enthält den aktuellen Stand meiner Visu-Entwicklung für HA. Derzeit funktional:

> Hinweis: Bitte nicht über die Temperaturen in meinen Screenshots wundern - meine Bastel-Trovis ist nicht an eine wirkliche Heizung angeschlossen, alle Sensoren messen nur Raumteperaturen.

- Links oben: Bild des aktuellen Heizungsschemas wird bei Statusänderungen umgeschaltet, die angezeigten Sensorwerte sind _live_. Zur Anpassung nach Bedarf den Template Sensor [trovis_regler_gesamtstatus](https://github.com/Tom-Bom-badil/samson_trovis_557x/blob/fb5b95a82fc74c09eb616c466df82a3f73f5a9c4/HomeAssistant/trovis557x/template_sensors.yaml#L8C7-L8C34) anpassen und unter [www/trovis557x/images/status*.svg](https://github.com/Tom-Bom-badil/samson_trovis_557x/tree/master/HomeAssistant/www/trovis557x/images) eigene Bilder einfügen.
- Links unten: Alle angezeigten Werte inkl Position der Reglerknöpfe, Heizkurve mit Umschaltung Tag-/Nachtsoll, Temperaturen und deren Historie, Reglertyp + Firmware usw sind _live_ und kommen direkt aus dem Regler. Es gibt aber noch etliche Punkte, die ich hier noch implementieren will.
- Rechts: Die Plots sind zwar in der Rohfassung bereits fertig, werden allerdings erst später nachgereicht.

![image](https://github.com/user-attachments/assets/534518c6-ca7d-4575-a9d6-43975fd17a32)

![image](https://github.com/user-attachments/assets/14e4dc7b-dc75-4589-ae4d-8b718566ab95)

# **Datei seitenaufteilung.yaml**

Ziel: Eine Konzept für die Aufteilung der Reglervisualisierung mit automatischer Anpassung an verschiedene Auflösungen (Heizungsschema interaktiv links oben, Reglerbild interaktiv links unten, rechts 3 Graphen mit Export-Funktionen etc).

Das Grundgerüst:
![seitenaufteilung](https://github.com/user-attachments/assets/374489ba-a67d-4748-b063-ee1df406f228)

Heizung aus (Status 0):
![seitenaufteilung_status_0](https://github.com/user-attachments/assets/af327bf7-d65c-4389-8d86-f91769436e28)

Heizbetrieb (Status 1):
![seitenaufteilung_status_1](https://github.com/user-attachments/assets/d53d4dff-0039-4419-b8c1-e6f99d5e1e1e)

Warmwasserbereitung (Status 2):
![seitenaufteilung_status_2](https://github.com/user-attachments/assets/ec061fe8-5640-43bb-b2e6-92120e75610d)

# **Datei reglerbild_interaktiv.yaml**
Ziel: Darstellung einer 5575/5576/5579 mit interaktiven Elementen und der tatsächlichen Heizkurve und aktuellem VL als plotly-Graph.

![reglerbild_interaktiv](https://github.com/user-attachments/assets/d9cff9b5-2bd7-4564-8b1c-4be8c340e9a5)

# **Datei plotly.yaml**
Ziel: Einbindung eines Graphen per plotly. Die Plotly-Bibliothek ist extrem gut dokumentiert und meiner Meinung nach nicht so buggy und deutlich flexibler / mächtiger als die üblicherweise verwendenten Lösungen wie HistoryGraphCard oder ApexCharts. Doku [hier](https://plotly.com/javascript). ACHTUNG! Die Beispieldatei enthält einen Datensimulator, der für 48h Daten generiert (zur Winterzeit --> daher sieht man zur Sommerzeit eine Stunde Versatz bzw. rechts einen 1h freien Bereich). Für die Visualisierung von Echtdaten muss die entsprechende entity: statt der fn: angebunden werden. Für einen Plot sollte die Entity bereits historische Werte aus einer Datenbank liefern.

Bereich R1 (rechts oben):
![plotly_1](https://github.com/user-attachments/assets/4e264bbf-5d39-43ae-a783-4ce92bb04e4d)

Heizkurve auf dem Regler:

![plotly_2](https://github.com/user-attachments/assets/5bc4732e-2dc4-48da-b3d8-2964ac58fbba)
