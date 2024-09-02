# install

Installation de Symfony dernière version stable avec la plupart des bibliothèques pour un site web :

    symfony new NomDuDossier --webapp

Lancement du serveur :

    cd NomDuDossier
    
    symfony serve -d

Update des bibliothèques :

    composer update

Création d'un contrôleur

    php bin/console make:controller HomepageController

Voir les routes

    php bin/console debug:route

Changement de la route en annotation (Attribut depuis PHP 8)

```PHP
# src/Controller/HomepageController.php

// racine

#[Route('/', name: 'app_homepage')]
```