# Pt1.5: Docker + MongoDB - Backend d'una botiga en línia

[cite_start]Aquest projecte consisteix en la construcció d'un entorn de bases de dades NoSQL utilitzant MongoDB executat dins de contenidors Docker[cite: 5]. [cite_start]L'objectiu és simular el backend d'una botiga en línia, gestionant des de la configuració de l'entorn fins a la realització de consultes avançades[cite: 6].

## Prerequisits

Per poder replicar aquest entorn, és necessari disposar del següent programari:

* **Docker**: Versió 20.10 o superior.
* [cite_start]**Docker Compose**: Versió 2.0 o superior[cite: 54].
* [cite_start]**Git**: Per a la gestió del repositori[cite: 44].
* **WSL2 (Windows Subsystem for Linux)**: Recomanat si s'executa en entorns Windows.

## Instruccions d'instal·lació i posada en marxa

1. **Clonar el repositori**:
   ```bash
   git clone <url-del-teu-repositori>
   cd practica-mongodb