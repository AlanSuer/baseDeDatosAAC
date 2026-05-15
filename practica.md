# Respostes a les preguntes teòriques - Pt1.5 MongoDB y captures

## Bloc 0

![alt text](/images/image.png)

![alt text](/images/image-1.png)

---

## Bloc 1: Configuració Docker Compose

**1. Quina és la diferència entre docker run i docker compose up?**
`docker run` s'utilitza per iniciar un únic contenidor des del terminal, introduint manualment els paràmetres a cada execució. `docker compose up` llegeix el fitxer declaratiu `docker-compose.yml` per orquestrar i iniciar múltiples contenidors alhora de forma automatitzada.

**2. Per a què serveix la instrucció depends_on? Garanteix que el servei dependent estigui completament operatiu?**
Serveix per establir l'ordre d'arrencada entre contenidors. No garanteix que el servei estigui operatiu; només indica que el contenidor s'ha iniciat, però no comprova si el procés intern (com el motor de la base de dades) ja pot acceptar connexions.

**3. Explica quina és la diferència entre una xarxa bridge per defecte i una xarxa personalitzada.**
La xarxa `bridge` per defecte permet comunicació per IP, la qual pot canviar. Una xarxa personalitzada proporciona resolució DNS automàtica, permetent que els contenidors es comuniquin pel seu nom (ex: `mongodb-botiga`), a més d'oferir millor aïllament.

![alt text](/images/image-2.png)

![alt text](/images/image-3.png)

---

## Bloc 2: Model de dades, volums i persistència

**Prova de persistència (Captures de pantalla)**
![alt text](/images/image-4.png)
![alt text](/images/image-5.png)
![alt text](/images/image-6.png)
![alt text](/images/image-7.png)

**1. Què passaria si no definíssim cap volum al docker-compose.yml? Fes la prova i documenta el resultat.**
Si no definim un volum, les dades s'emmagatzemen a la capa d'escriptura temporal del contenidor. En fer un `docker compose down`, el contenidor s'elimina i totes les dades inserides es perden definitivament.

![alt text](/images/image-8.png)
![alt text](/images/image-9.png)

**2. Explica la diferència entre un volum named (amb nom) i un bind mount. Quan convé usar cada un?**
Un volum *named* és gestionat completament per Docker en una ubicació interna, ideal per persistir dades de bases de dades sense dependre del sistema operatiu host. Un *bind mount* enllaça una ruta específica del host amb el contenidor, sent ideal per carregar fitxers de configuració o scripts de codi font (com la carpeta `./mongo-init`).

**3. Diferència entre l'estratègia embedding i referència amb exemples nous.**
* **Embedding**: S'utilitza per dades que pertanyen a una única entitat i es llegeixen juntes. Exemple: Un document `factura` que conté un array amb les `linies_factura`.
* **Referència**: S'utilitza per dades compartides o que creixen indefinidament. Exemple: Una col·lecció `autors` i una col·lecció `llibres` on cada llibre guarda l'`id_autor` en lloc de duplicar les dades de l'autor.

**4. Quina estratègia has fet servir en la col·lecció comandes i per quin motiu.**
He utilitzat l'estratègia de referència. Les comandes guarden el `client_id` i un array de `productes_id`. El motiu és evitar la duplicació de dades: la informació del client i del producte té un cicle de vida independent i s'actualitza per separat (per exemple, si el client canvia de telèfon o el producte canvia de preu).