# ACTIVITAT 01 - Cas d'ús: Curs de programació

## 1 Part pràctica: Configuració del servidor

Primerament, hem creat una maquina rocky linux nova anomenada: curs-coding-asv01 i que finalitza amb la IP .109:

<img width="1436" alt="Captura de Pantalla 2022-10-01 a las 16 38 10" src="https://user-images.githubusercontent.com/38278207/193414642-8c76eb30-1c34-4689-857c-de1b1df9bd54.png">

### Creareu un usuari admin que pugui esdevenir root i SIGUI l’únic usuari que pot entrar al sistema de forma remota per SSH.

- Usuari: admin 
- Password: adminadmin.

<img width="1017" alt="Captura de Pantalla 2022-09-29 a las 20 49 47" src="https://user-images.githubusercontent.com/38278207/193117424-40391aaf-e53e-4b99-9fbf-22ff2472cdb6.png">

Li assignem permissos de superusuari dins del ``` sudo visudo ```:

<img width="1017" alt="Captura de Pantalla 2022-09-29 a las 20 50 43" src="https://user-images.githubusercontent.com/38278207/193117725-fa9bcf3f-8966-4077-b069-0236fea589e8.png">

### Els professors han de tenir el seu directori inicial a /home/professorat/nom_professor.

Afeguirem dos professors al home de professorat: 

- groupadd -g 2 professorat
- useradd -d/home/professorat/jordi -m jordi
- useradd -d/home/professorat/jesus -m jesus

 ![image](https://user-images.githubusercontent.com/79162978/193696747-3acf2f55-bc21-4a41-a7b3-c11fb5ba5fdd.png)

 
### Els alumnes han de tenir el seu directori inicial a /home/alumne/nom_alumne.

- useradd -d/home/alumne/samantha -m samantha
- useradd -d/home/alumne/paula -m paula
- useradd -d/home/alumne/alex -m alex
- useradd -d/home/alumne/jaimito -m jaimito

 ![image](https://user-images.githubusercontent.com/79162978/193696833-f15c9f60-21f2-4104-9751-a480adcbe2fa.png)
 

### Els professors han de poder (rwx) a tots els directoris /home/alumne/

S'ha donat el máxim dels permisos al grup de professorat: 

 ![image](https://user-images.githubusercontent.com/79162978/193698089-f1f5603f-7033-4e7d-8b76-d7ad0b351219.png)

Seguidament, amb les següents comandes hem establit a les carpetes dels alumnes permisos als professors: 

 ![image](https://user-images.githubusercontent.com/79162978/193698265-1a07823f-2894-4a4c-a786-83a2e22fa6d0.png)

A continuació, hem fet la comanda ```ls -la ``` per veure els permissos: 

 ![image](https://user-images.githubusercontent.com/79162978/193698417-a7cfa5a5-bbc4-44d8-80a0-8437f99fcfac.png)


- Alternativa per posar permisos:

![image](https://user-images.githubusercontent.com/38278207/193120164-86008861-9be6-4b8b-9d75-3f5a0ba91d6c.png)

``` chmod 777 ```

### Els alumnes únicament han de poder utilitzar els seus directoris inicials

Perque els alumnes no puguin accedir al grup dels professors: 

 ![image](https://user-images.githubusercontent.com/79162978/193698702-8b42335c-f598-4861-9a97-1f14fd23edf8.png)
 

# JupiterLab

### Configureu un servidor jupyterlab per poder accedir a un entorn per a treballar.

- Primer de tot farem la comanda de:  ``` sudo dnf -y update ``` 

- Seguidament, instal·larem python 3.9 al servidor: ``` sudo dnf install python39 ``` 

- Verificarem la versió que se'ns ha instal·lat al server: ``` python3.9 --version ``` 

 ![image](https://user-images.githubusercontent.com/79162978/193466517-b30fc9e8-dbc2-4aa9-92d8-dd0652779d2c.png)

- Instal·larem per poder fer servir pip i jupiterlab: ``` sudo dnf install nodejs npm ```
    
![image](https://user-images.githubusercontent.com/79162978/193466625-58208203-d242-4707-93d2-c84f019d4aae.png)

- A continuació, farem les següents comandes:  

 ``` python3 m pip install jupyterhub ```

 ``` npm install -g configurable-http-proxy ```

 ``` python3 -m pip install jupyterlab notebook ```

- Arrencarem el jupiterlab amb la comanda: ``` jupyterhub ``` 
- I ens logeem amb admin adminadmin
  ![image](https://user-images.githubusercontent.com/79162978/193617157-926d0089-acb8-405a-a01a-35e1c6cb69dc.png)

- Crearem el fitxer de config (aquest pas és innecesari): ``` jupyterhub --generate-config -f jupyterhub_config.py ```

- Arrencarem el jupyterhub amb el config (aquest pas és innecesari): 

  ![image](https://user-images.githubusercontent.com/79162978/193467745-f41af1a8-22fd-4b00-8aaa-406c378a4391.png)

- Tots els alumnes/professors han de poder accedir al servei via web, però no fer login al sistema per terminal.

- Bloquejarem l’accés al jupyterlab al Jaimito: 

- Hem editat el fitxer de configuració ``` vim jupyterhub_config.py ``` tenint en compte tot el que es demana de la següent manera:

<img width="1017" alt="Captura de Pantalla 2022-10-03 a las 12 07 48" src="https://user-images.githubusercontent.com/38278207/193552456-0da684d8-e067-4307-a344-86850e2a2c2d.png">

## Links de interés:

- https://jupyterhub.readthedocs.io/en/stable/getting-started/security-basics.html
- https://jupyterhub.readthedocs.io/en/stable/quickstart.html

***

## Pregunta 2: Investigar eina psacct

``` psacct ``` es una eina de codi obert que serveix per monitoritzar les activitats que tenen els usuaris sobre un sistema, entrades i surtides, activitat... ens permet obtenir info com:

- Monitoritzar les activitats de l'usuari.

- Desplega les ordres que es fan servir. 

- Desplega un informe sobre els recursos que s'utilitzen al sistema.

- Ens permet observar quant temps porten connectat els usuaris al sistema

- Acct i psacct no consumeix recursos de la màquina, llavors millorent el rendiment gracies al que ens donen

De manera que com a sysadmin o profes del grup, ens pot servir per saber "qui esta a classe" i quanta estona, des de quan esta connectat l'alumne, que ha fet, etc. En general, tenir un control absolut sobre la asistencia de l'alumnat

### Com instal·lar-lo?

``` yum install psacct ```

```chkconfig psacct on ```

Cal esperar una mica i anar jugant amb diversos usuaris fent comandes, segons quina comanda posteriorment fem servir, no veurem resultat 😅

### Com fer-lo servir?

#### Comanda ac

La comanda ``` ac ``` ens dona el temps total en hores d'inici i tancaments de sessió dels usuaris.

I podem refinar més la comanda posant-li paràmetres:

``` ac -d ``` ens dona el temps total per dia 

``` ac -p ``` ens dona el temps per usuari, una comanda molt interessant com a "profe"

<img width="1017" alt="Captura de Pantalla 2022-10-01 a las 17 07 01" src="https://user-images.githubusercontent.com/38278207/193415839-41979726-f689-4d01-a1d8-0de22eacf42a.png">

(Amb el curs en marxa i alumnes a classe, la sortida de les comandes seria molt mes representativa 😁)

#### Comanda sa

Eina molt interessant ja que ens resumeix les comandes que han utilitzat els usuaris, ideal per "veure que han fet els alumnes a classe"

Si executem la comanda ``` sa ```

<img width="1017" alt="Captura de Pantalla 2022-10-01 a las 17 19 06" src="https://user-images.githubusercontent.com/38278207/193416280-f53851f5-7a54-4c4f-8cd6-1e484bfed85e.png">

De cada columna, podem extreure que que:

- 1a: Quantitat de vegades que s'ha executat l'ordre.

- 2a: Temps real en minuts.

- 3a: És el total dels minuts en format de CPU del sistema de cada usuari.

- 4a: Quantitat de nucli usat.

- 5a: A la darrera columna veiem l'ordre executada.

Per veure la info de manera individual, podem fer ``` sa - u ```:

<img width="1017" alt="Captura de Pantalla 2022-10-01 a las 17 19 40" src="https://user-images.githubusercontent.com/38278207/193416309-a15b2ea7-e086-425f-9eec-4ed8fcb6ed78.png">


#### Comanda lastcomm

Semblant a l'anterior, més concret, ens dona les comandes utilitzades segons l'usuari que li passem per paràmetre. 

<img width="1017" alt="Captura de Pantalla 2022-10-01 a las 17 18 23" src="https://user-images.githubusercontent.com/38278207/193416249-f24e65f4-7da7-4c70-94f1-ed350f61d927.png">

#### Comanda lastb

Ens dona últim accessos al sistema, indicant la data i hora, es molt concret:

<img width="1017" alt="Captura de Pantalla 2022-10-01 a las 17 14 23" src="https://user-images.githubusercontent.com/38278207/193416101-aa6a237c-80ac-46b5-837f-feaccce938ee.png">

#### Comanda accton on

Ens permet habilitar o des-habilitat processos d'usuari

<img width="1017" alt="Captura de Pantalla 2022-10-01 a las 17 15 59" src="https://user-images.githubusercontent.com/38278207/193416167-705bca79-f0ed-453c-a69c-06b62fec22e0.png">

#### Comanda aureport

Resum general del sistema, ens dona moltissima info:

<img width="1017" alt="Captura de Pantalla 2022-10-01 a las 17 26 36" src="https://user-images.githubusercontent.com/38278207/193416571-18e81c32-0d16-45a1-8e4c-0bf86e2cb639.png">

Podem perfilar molt més la comanda amb els parametres:

- ``` aureport -l ``` : Si tenim servidor gràfic veurem entrades corresponents a les sessions iniciades a gdm3, kde, etc

- ``` aureport -n ``` : Ens dona un resum d'anomalies 

## Links de interés:

- https://www.solvetic.com/tutoriales/article/2940-monitorear-actividad-de-usuario-con-acct-o-psacct/
- https://www.elarraydejota.com/supervision-del-sistema-con-psacct-acct-y-audit/
- https://www.unixmen.com/monitoring-users-activity-using-psacct-or-acct-tools-in-linux/

