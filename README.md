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

## Création d'une entité

```bash
php bin/console make:entity

 Class name of the entity to create or update (e.g. VictoriousPuppy):
 > Article
Article

 Add the ability to broadcast entity updates using Symfony UX 
 Turbo? (yes/no) [no]:
 >

 created: src/Entity/Article.php
 created: src/Repository/ArticleRepository.php


 New property name (press <return> to stop adding fields):
 > Title
  Field type (enter ? to see all types) [string]:
 >


 Field length [255]:
 > 160

 Can this field be null in the database (nullable) 
 (yes/no) [no]:
 >

 updated: src/Entity/Article.php

 Add another property? Enter the property name 
 (or press <return> to stop adding fields):
 > text
 
 Field type (enter ? to see all types) [string]:
 > text
text

 Can this field be null in the database (nullable) 
 (yes/no) [no]:
 >

 updated: src/Entity/Article.php

 Add another property? Enter the property name (or press <return> to stop adding fields):
 > dateCreate

 
 Field type (enter ? to see all types) [string]:
 > datetime
datetime

 Can this field be null in the database (nullable) 
 (yes/no) [no]:
 > yes

 updated: src/Entity/Article.php

 Add another property? Enter the property name 
 (or press <return> to stop adding fields):
 > datePublish

 
 Field type (enter ? to see all types) [string]:
 > datetime
datetime

 Can this field be null in the database (nullable) 
 (yes/no) [no]:
 > yes

 updated: src/Entity/Article.php

 Add another property? Enter the property name 
 (or press <return> to stop adding fields):
 > isPublished

 Field type (enter ? to see all types) [boolean]:
 >

 Can this field be null in the database (nullable) 
 (yes/no) [no]:
 >

 updated: src/Entity/Article.php

 Add another property? Enter the property name 
 (or press <return> to stop adding fields):
 >

  Success!


 Next: When you're ready, create a migration with 
 
php bin/console make:migration


```
