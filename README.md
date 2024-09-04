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

## Création de `.env.local`

    cp .env .env.local

Il ne sera pas mis sur github car il est dans le `.gitignore`

puis modifier la ligne `DATABASE_URL` pour la connexion à la base de données pour activer mysql  :
    
```env
DATABASE_URL="mysql://root:@127.0.0.1:3306/entitysymg2?serverVersion=8.3.0&charset=utf8mb4"
# DATABASE_URL="mysql://app:!ChangeMe!@127.0.0.1:3306/app?serverVersion=10.11.2-MariaDB&charset=utf8mb4"
# DATABASE_URL="postgresql://app:!ChangeMe!@127.0.0.1:5432/app?serverVersion=16&charset=utf8"

```

## Création de la base de données

    php bin/console doctrine:database:create

## Création de la migration

    php bin/console make:migration

## Exécution de la migration

    php bin/console doctrine:migrations:migrate

ou

    php bin/console d:m:m


## Création d'un CRUD

    php bin/console make:crud Article

    nom : ArticleCrud

https://127.0.0.1:8000/article/crud

## Modification du formulaire

```PHP
<?php
# src/Form/ArticleType.php

namespace App\Form;

use App\Entity\Article;
use Symfony\Component\Form\AbstractType;
use Symfony\Component\Form\FormBuilderInterface;
use Symfony\Component\Form\Extension\Core\Type\TextareaType;
use Symfony\Component\Form\Extension\Core\Type\DateTimeType;
use Symfony\Component\OptionsResolver\OptionsResolver;

class ArticleType extends AbstractType
{
    public function buildForm(FormBuilderInterface $builder, array $options): void
    {
        $builder
            ->add('title')
            ->add('text', TextareaType::class)
            ->add('dateCreate', DateTimeType::class, [
                'widget' => 'single_text',
                'data'=> new \DateTime(),
            ])
            ->add('datePublish', null, [
                'widget' => 'single_text',
            ])
            ->add('isPublished')
        ;
    }

    public function configureOptions(OptionsResolver $resolver): void
    {
        $resolver->setDefaults([
            'data_class' => Article::class,
        ]);
    }
}
```

## Pour les templates

```yaml
# config/packages/twig.yaml
twig:
    form_themes: ['bootstrap_5_layout.html.twig']
```