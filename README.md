# TP5
le but ultime de ce dernier Tp:
Voir comment créer un web service
Comment déployer un web service a travers un serveur JawWS
Comment déployer un web service basée sur SOAP dans une application Spring
A l'aide d'un browser On va consulter le WSDL pour l'analyser et voir sa structure
Et puis on vas voir comment tester le web service en utilisant un outil qui s'appelle SoapUI
Ensuite on va créer un client java qui permet de consommer le webservice
On commence par créer un simple projet Java:ws-soap-fsm
Ensuite on effectue la création d'un package nommée ws et ce dernier contient une classe dont son nom est:BanqueService et Compte
Donc on commence par le contenu de la classe Compte:
![image](https://github.com/baayaouiimane/TP5/assets/167249908/c49d1b74-a404-4ba7-bc1e-ff3b7f72ac91)
![image](https://github.com/baayaouiimane/TP5/assets/167249908/c6addeac-5578-4499-aaf9-e8c0c049aed7)
Et voici le contenu de BanqueService:
![image](https://github.com/baayaouiimane/TP5/assets/167249908/bd827a7a-cee5-4e02-a125-8ef4f1ea317f)
Si vous remarquez la notation WebService n'appartient pas a jdk par défaut, donc pour résoudre ce problème il faut ajouter une dépendance dans le fichier pom.xml:
![image](https://github.com/baayaouiimane/TP5/assets/167249908/ec3573df-2a8f-40de-bccb-717677304fe6)
Et donc en revenant a la classe BanqueService le problème sera résolu:
![image](https://github.com/baayaouiimane/TP5/assets/167249908/6350da64-733b-4c79-af88-40d194481053)
![image](https://github.com/baayaouiimane/TP5/assets/167249908/faf4a2c7-9cc1-4b65-be82-b9c657443529)
Maintenant on a besoin de déployer le webservice,pour déployer ce dernier donc on va créer notre propre serveur:SserverJWS
![image](https://github.com/baayaouiimane/TP5/assets/167249908/9cdfb565-2df7-488d-bd0c-8cd1a5a24767)
En démarrant le serveur:
![image](https://github.com/baayaouiimane/TP5/assets/167249908/d52d4c7c-30d0-4a06-95df-3d6fecff6c1a)
Cette fois ci on démarre un naviguateur web et on va demander le WSDL:
![image](https://github.com/baayaouiimane/TP5/assets/167249908/f2f2a018-185a-42c9-a1e3-aa7aa7850ebf)
Cette fois ci en visitant:http://localhost:9090/?wsdl on aura:
![image](https://github.com/baayaouiimane/TP5/assets/167249908/3ade0b5d-d18c-47a6-9702-e979d4647c14)
Cette fois ci en visitant :http://localhost:9090/BnaqueWS?wsdl
![image](https://github.com/baayaouiimane/TP5/assets/167249908/81cb5e57-0c6d-4fb0-b528-1d72fae5b0cb)
En visitant:http://localhost:9090/?xsd=1
![image](https://github.com/baayaouiimane/TP5/assets/167249908/605af426-a444-4b66-99e0-6927ca091ef8)
Pour tester le webservice nous allons utiliser un outil nommée SoapUI:
Tout d'abord il faut installer :SOAP UI Downloads.
En cliquant sur request1 qui se trouve dans ConversionEuroToDH:
Donc on a envoyé la requete et on a recu la requete comme il apparait ci dessous:
![image](https://github.com/baayaouiimane/TP5/assets/167249908/49d35ce4-3257-42ae-a853-dbbcc352e37e)
En faisant un autre test on aura:
![image](https://github.com/baayaouiimane/TP5/assets/167249908/3fb99367-446e-4b4c-9dd0-925ebf39a1a1)
En cliquant sur request1 qui se trouve dans getControle:
![image](https://github.com/baayaouiimane/TP5/assets/167249908/bb1ec9ff-7942-4bc9-8916-c5d26ddf794c)
On remarque que la date de création n'est pas bonne autrement dit elle est vide parce qu'on a utilisé le format LocalDate:
On doit apporter des modifications a la classe Compte.java:
![image](https://github.com/baayaouiimane/TP5/assets/167249908/1983e32e-8782-4503-a90a-793e812b91db)
![image](https://github.com/baayaouiimane/TP5/assets/167249908/2e03becf-8d1b-4b57-8a97-3e005408ff65)
![image](https://github.com/baayaouiimane/TP5/assets/167249908/dd7539a9-3204-4090-bf95-7befaabf15cd)
Et on doit apporter aussi des modifications a la classe BanqueService.java:
![image](https://github.com/baayaouiimane/TP5/assets/167249908/e30ceb35-18de-4e0e-abdd-69212407857f)
Ensuite on redémarre le serveur:
![image](https://github.com/baayaouiimane/TP5/assets/167249908/52afb13f-5698-4056-938e-f198b5485edc)
Par la suite on va faire un test:
![image](https://github.com/baayaouiimane/TP5/assets/167249908/d1c086aa-b5d9-4890-8560-bdb22ee41217)
En cliquant sur request1 qui se trouve dans getControle:
![image](https://github.com/baayaouiimane/TP5/assets/167249908/021b6ea9-c88f-4c10-a7a1-b7ebfb1e82f7)
En cliquant sur request1 qui se trouve dans listComptes:
![image](https://github.com/baayaouiimane/TP5/assets/167249908/00307a51-f428-49f6-bb1a-9273837e8bb8)
Et donc cette fois on est chargé de créer un client java qui permet de consommer le webservice: on doit créer un module nommé client-ws a l'intérieur du projet:
On a commence par ajouter la dépendance au fichier pom.xml:
![image](https://github.com/baayaouiimane/TP5/assets/167249908/6a48c694-49a4-4c93-9fed-74ef50ab2e60)
Pour créer le client on a besoin du WSDL et a partir de ce dernier on pourra générer un proxy(ensemble de classe générer a partir du WSDL qui vont permettre a mon app java de communiquer
avec le webservice)et donc la génération du proxis se réalise comme suit:
il faut installer Jakarta EE:Web Services(JAX-WS)
Après l'installation on a:
![image](https://github.com/baayaouiimane/TP5/assets/167249908/76772290-9326-4e5f-a4b8-19b9f0131c34)
Ensuite dans l'application cliente on a :
![image](https://github.com/baayaouiimane/TP5/assets/167249908/67155d90-cf1c-42ea-a07e-e5f6465bbe94)
En exécutant on obtient le résultat suivant:
![image](https://github.com/baayaouiimane/TP5/assets/167249908/beb9c523-fef5-4631-8c0d-b0cc9b450225)
Ensuite on a:
![image](https://github.com/baayaouiimane/TP5/assets/167249908/76cb658e-e305-4765-b78a-97767e314ff3)
Et en exécutant le code on obtient:
![image](https://github.com/baayaouiimane/TP5/assets/167249908/2e985442-089c-4f1e-8668-dbd53d84031d)







