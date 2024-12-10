# eX Modelight 2024

## Date
9, 10, 11 Décembre

## Effectifs
24 max

## Application

4 octobre 1er deadline

18 2nd deadline 
25 octobre - notification

## Programme

Une demie journée = 3H maxi , une demie-heure de pause dans chaque demie journée.

## Instances

Clés cluster : 
group 1/2 : ML
group 3/4 : JR
group 5/6 :
group 7/8 :

## TPs

Dossier pour uploader et partager les TPs en tgz :
https://nextcloud.openmole.org/apps/files/files/15547?dir=/exmodelo-2024

## Demie journée 1.1 : Romain 

### Accueil café viennoiserie 

faire établir une facture 

:::info
**Opening course**
Complex systems modelling and simulation
:::

**Présentations:**
- 9h30-11h30 Cours théorique :  du modèle à son exploration https://hackmd.openmole.org/6NBcQnvsSkm3XHOHE2Ypqg# [name=RR]
- 0h20 Une pause
- 0h20 Le modèle Z (fiche simplifiée du modèle ? ) cf https://hackmd.openmole.org/QWBcNSi7TXqOcKVhC1Cl2Q# [name=RR]
- 0h20 Bornéo https://hackmd.openmole.org/p/orangOutanExModelo# [name=ML]

**Objectif de fin de demi-journée 1** : 
- théorie de l'exploration (pourquoi il faut explorer) notion d'heuristique,  limites de l'explo systématique, que faire des résultats d'exploration ? Modèle *ants* pris comme exemple pour le cours
- présentation du modèle Z

## Demie journée 1.2 : Apprendre à utiliser OM

:::info
**Getting started** 
Starting with OpenMOLE: model embedding and exploration
:::

**Objectifs de début de demi-journée 2** :
- devenir  familier avec un usage de base d'OpenMOLE : syntaxe du sampling, variable, hook + GUI execution, GUI sorties, GUI fichiers 
- J'ai entrevu les limites du sampling direct
- je sais où se trouve les scripts dans la GUI, 
- je sais retrouver les résultats et les afficher
- je sais prendre les résultats pour les traiter avec mes outils de vizu/stats

**Déroulé [Part I] 0h45**
- DSL [name=ML] https://hackmd.openmole.org/W5mdU394Qpq24nkHOT8hGg#
- GUI OM [name=ML] https://hackmd.openmole.org/oiiErkP6RviUiZU67XG9fA#
:::warning
les supports de GUI OM (guided tour of the interface) sont à rafraîchir
:::

**Déroulé [Part II] 1h**

- TP Exploration [name=JR] : réplications, plan complet sur Z cooperation https://hackmd.openmole.org/fbqAdloySTeUhBoJ-MMZiA


*Il faut leur faire sentir les limites du plan complets ou des plans à façon, même avec LHS.*

**Pause 15min**

**Déroulé [Part III] 1h**
En groupe: 

- [name=CdB] pour Python
- [name=JR] pour R  ([TP de Paul l'année dernière](https://gitlab.openmole.org/exmodelo/courses/-/tree/master/Practical_session_R_model_inOM?ref_type=heads)) -> r-logisticregression in market (joint avec python)
- [name=ML] pour NetLogo
- [name=PC] pour GAMA 
- [name=MC] [Julia](https://hackmd.openmole.org/ui1gNooaRfWEgG3avBtUVw?both) 
- [name=JR] Scilab ?

pour les autres techno on attend les réponses et on préparera en septembre

(On fournit des modèles en scala, R, python, julia , dont on connaît les entrées et les sorties , avec script OM associés )


TODO : 

petit support sur les prérequis pour que "mon" modèle aille dans OM : 
pas de gui, il faut un headless, il faut installer les lib à part , pas dans l'execution du modèle.
Il faut que l'éxécution soit "unitaire", pas de replications ou de boucles sur l'input space à l'intérieur du modèle.

modèle python avec un fichier en entrée: 

- des entiers 
- des doubles
- un fichier 

et en sortie : 

- un fichier (au moins un ) 
- un vecteur de double 
- une matrice ? 



**Objectif de fin de demi-journée 2** : 
- être rassuré : «je connais cette techno XXX, et OM peut travailler avec XXX», si besoin c'est faisable


## Demi journée 2.1 : optimisation générale (NSGA2)

https://hackmd.openmole.org/siWhKUt7TbexZKUKhthbEg#

- [name=RR]

:::info
**Calibration & Optimisation**
Sampling the input space using optimisation heuristics
:::
L'optimisation comme technique générale pour dépasser les limites vues la veille

Zombies calibrage 3 params, 1 objectif
Zombies optim armé, 2 objectifs

### Déclinaisons de l'optim suivant le type de sorties: 

cas simple : calibrer sur des doubles 
cas du fit de trajectoires / séries temporelles (descripteurs)
cas du fit de distributions 

###  Utilisation de l'optim pour modéliser : 
 
La chose à saisir : parfois l'optim ne "marche pas" : on peut modifier le modèle pour dépasser la limite mise en évidence par la mauvaise calibration  
 
 Exemple : 
  - activer/desactiver un mécanisme 
  - faire varier l'espace 


Un jupyter et/ou des scripts + face validity sur demo modèle zombie 



**Objectif partiel de fin de demi-journée 3** : «J'ai fait le lien entre résolution de problème et optimisation de quelque chose. Je sais qu'OM sait faire de l'optimisation  avec NSGA2»


## Demi journée 2.2 : Panorama des méthodes puis TP en autonomie sur un nouveau modèle


- **Part I: 1/3 = 1h** [name=ML]
Ouverture sur panorama complet des méthodes d'OM. Saltelli, Morris , PSE (à détailler plus ) & OSE

:::info
**Guided tour of OpenMOLE Methods**
Get an overview of advanced OpenMOLE methods to evaluate your model
:::

$\rightarrow$ use the new spiral synoptic method representation

Slides : 
[exmodelo summary of methods](https://hackmd.openmole.org/p/methodOverview#/)
[Saltelli and Morris excerpts from JR](https://raw.githubusercontent.com/openmole/exmodelo-courses/master/sensitivity/sensitivity.pdf)
[resources from romain](https://hackmd.openmole.org/p/mIwn79YMS#/53)




- **Part II: 2/3 = 2h** [name=JR]


**Goal:** model the question into an optimization problem , use NSGA2 to answer it. On a new model (ants), developped in scala ([Link to the source](https://github.com/openmole/ants-scala)), each group formulates its own questions and proposes a method to answer it. For a better understanding of the model, they can explore the NetLogoWeb version [here](https://www.netlogoweb.org/launch#https://www.netlogoweb.org/assets/modelslib/Sample%20Models/Biology/Ants.nlogo).

**Examples of questions:**
    - Calibrate on food consumption values (files on demand)
    - Inverse problem on the location of food sources
    - optimise the performance of ants to eat as fast as possible
    - balance between food sources
    - given a fixed amount of food, what repartition across different sources? (varying number, size and position)
    - optimise the chemical perception parameters (ants saturation for example), how does this interacts with the "optimum" for evaporation/diffusion?
    
**Provided to the students:** [archive](https://nextcloud.openmole.org/s/Nnfn5zSxHcW4FYQ/download) with the model plugin and a basic script to run the model




## Demi-journée 3.1 & 3.2 : OpenMOLE on your own model


## Com'

### Content


### Destinataire
- [ ] ISC-PIF [name=ML]
- [x] Géocitées [name=RR]
- [x] Payotes via Myriam [name=RR]
- [x] Anne-Laure ISC [name=RR]
- [x] Réseau Gama - envoyé à Partrick pour relais [name=RR]
- [x] geotamtam [name=JR]
- [ ] quanti [name=ML]
- [x] EuroTQG [name=JR]
- [x] IGU Urban [name=JR]
- [x] LVMT - Florent [name=JR]
- [ ] CASA, UCL, Londres [name=JR]
- [x] IDM4SCO (https://sympa.inria.fr/sympa) [name=RR]
- [x] Devlog [name=RR]
- [x] Simsoc (https://www.jiscmail.ac.uk/cgi-bin/webadmin?A0=simsoc) [name=RR]
- [x] Alumni exModelo [name=ML]
- [x] Computational social sciences (https://computational-social-science.org/mailing_list.html) [name=RR]
- [ ] INRAE via Sophie et Isabelle [name=ML]
- [x] Réseau calcul CNRS [name=ML]
- [x] CIRAD [name=ED]
- [x] Cyril Piou [name=ED]
- [ ] Uta Berger [name=ED]
- [x] IRIT toulouse via Fred Amblard et Benoît Gaudou [name=PC]
- [x] Santa Fé Institute [name=ML]
- [x] IGN: Lastig [name=PC]
- [x] IGN: Innovation F. Fuchs [name=PC]


## Annoucement mail 


Object: Model Exploration with OpenMOLE: eX Modelo workshop

Dear all,

Following the success of the 2023 edition of the eX Modelo school, we are glad to announce that the school is coming back this year.

The eX Modelo Workshop will be a 3 days research workshop dedicated to the exploration of simulation models (sensitivity analysis, calibration, validation, etc.) that will be held from Monday 9th to Wednesday 11th December, 2024 at the Complex Systems Institute in Paris.

This teaching workshop is open to postgraduate students, engineers, academic researchers and businesses interested in modelling and simulation, regardless of their scientific field. The objective is give the tools for participants to become autonomous in exploring and validating their models.


The workshop will be led by a team of researchers with a recognised expertise in these interdisciplinary practices.

During these two days, you will discover step by step advanced methods for model exploration.

There will be theoretical courses as well as practical sessions to run these methods with various simulation models and programming languages.

The OpenMOLE platform (https://openmole.org), specially dedicated to the exploration of simulation models, will be used throughout the workshop for practical sessions.

The last day of the to workshop will be optional and dedicated to work on integrating your own model into OpenMOLE.


Important dates:

Applications before: October 4th, 2024
Shortlisting and notification of acceptance: October 25th, 2024
Participation in the workshop: December 9th, 10th and 11th, 2024

More details online at https://exmodelo.org/

Should you need further information, you can send us an email at school@exmodelo.org.


See you soon!


The organising team
