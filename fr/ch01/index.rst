===================
Introduction à Qt 5
===================

.. sectionauthor:: `jryannel <https://github.com/jryannel>`_, `brexis <https://github.com/brexis>`

.. issues:: ch01

.. note::

    Le code source de ce chapitre est disponible dans le ` dossier assets <../../assets>`_.

Ce livre vous entrainera à travers les differents aspects du développement d'une application Qt 5.x. Il met l'accent essentiellement sur la nouvelle technologie Qt Quick mais fournit également les informations necessaires pour le développement back-ends et d'extension C++ pour Qt Quick.

Ce chapitre donne une vue plus poussé de Qt 5. Il montre les différents modèles d'application disponibles pour les développeurs ainsi qu'une application démo pour avoir un aperçu des chapitres à venir. De plus, ce chapitre vise à fournir un large aperçu du contenu de Qt 5 et sur comment prendre en main les outils de Qt 5.


Preface
=======
.. rubrique:: Historique

Qt 4 a évolué depuis 2005 et a fourni une base solide pour des milliers d'applications aussi bien pour des systèmes complets desktop que mobile. Les habitudes d'utilisation des ordinateurs ont changé ces dernières années. Des ordinateurs de bureau aux ordinateurs mobiles de nos jours en passant par les ordinateurs portatifs. Le bureau classique est de plus en plus remplacé par des écrans mobiles tactiles connectés. Avec elles, les paradigmes de l'expérience utilisateur (UX) du bureau ont également changé. Pendant que, dans le passé, les interfaces utilisateurs (UI) Windows dominaient le monde, nous passons plus de temps de nos jours sur d'autres types d'écrans dotés d'un autre langage d'UI.

Qt 4 a été conçu pour satifaire le monde desktop avec un ensemble coherent de composants graphiques sur la majeur partie  des plateformes. Le défi pour les utilisateurs Qt a changé aujourd'hui et il se concentre plus à fournir une interface utilisateur basée sur le tactile axé sur la clientèle et à permettre une interface utilisateur plus moderne sur les principaux systèmes desktop et mobile. Qt 4.7 commença à introduire la technologie QtQuick qui permet aux utilisateurs de creer un ensemble de composants d'interface utilisateur à partir de simples éléments pour aboutir à un nouvel UI complet, axés sur la demande des consommateurs.

Qt5 Focus
---------

Qt 5 est une mise à jour complète de la version la plus réussie de Qt 4. Avec Qt 4.8, Qt 4 est vieux de près de 7 ans. Il était temps de développer un outil impréssionnant encore plus impréssionnant. Qt 5 se bases sur les points suivants:

* **Graphiques exceptionels**: Qt Quick 2 est basé sur OpenGL (ES) utilisant une implémentation de scene graph. La pile de graphiques recomposés permet de combiner des effets graphiques à une facilité d'utilisation d'un niveau supérieur jamais vu auparavant dans le domaine.

* **Productivité des développeurs**: QML et Javascript sont les principaux langages de création d'UI. Le C++ est utilisé en back-end. La séparation en Javascript et C++ permet une itération rapide pour que les développeurs front-end se concentrent mieux sur la création de belles interfaces utilisateur et aux développeurs back-end C++ de se concentrer sur la stabilité, la performance et d'étendre le temps d'exécution de l'application.

* **Portabilité Multi-plateformes**: Avec la technologie consolidée de Qt Plateform Abstraction, il est maintenant possible de porter Qt sur une gamme plus large de plateformes, plus facilement et plus rapidement. Qt 5 est structué autour du concept de Qt Essentials et de ses modules, ce qui permet au développeur d'OS de se focaliser sur les modules essentiels et conduit à un temps d'exécution tout à fait plus court.

* **Collaboration ouverte**: Qt est maintenant un véritable projet de open-gouvernance hébergé sur `Qt-Project <http://qt-project.org>`_. Le développement est ouvert et maintenu par la communauté.



Introduction à Qt5
==================


Qt Quick
--------

Qt Quick est le terme générique utilisé pour désigner la technologie d'interface utilisateur de Qt 5. Qt Quick en lui-même est une collection de diverses technologies:

* QML - Un langage de balisage pour les interfaces utilisateur
* Javascript - Le langage script dynamique
* Qt C++ - Une librairie c++ fortement renforcée et portable

.. image:: ../../en/ch01/assets/qt5_overview.png


Similaire à l'HTML, QML est un langage de balisage. Il est composé de balises appelées éléments QtQuick renfermés dans des accolades ``Item {}``. Il a été conçu dès le départ pour la création d'interface utilisateur, rapide et facile à lire pour les développeurs. L'interface utilisateur peut être améliorée avec du code Javascript. Qt Quick peut facilement être étendu avec votre propre fonctionalité native en utilisant Qt C++. En résumé, l'UI déclarative est appelé le front-end et les parties natives le back-end. Cela permet de séparer l'opération de calcul intensive et native de votre application de la partie interface utilisateur.

Dans un projet typique le développement front-end est en QML/Javascript et le code back-end, qui s'interface avec le système et qui s'occupe de la majeur partie du travail, est développé en Qt C++. Cela permet une répartition naturelle entre les développeurs orientés plus design et les développeurs fonctionels. Le back-end est typiquement testé avec le framework unitaire de Qt et exporté pour être utilisé par les développeurs front-end.


Assimiler une Interface Utilisateur
-----------------------------------

Créons une simple interface utilisateur avec QtQuick, qui met en valeur quelques aspects du langage QML. A la fin, nous aurons un moulin à vent en papier avec des lames rotatives.


.. image:: ../../en/ch01/assets/scene.png
    :scale: 50%


Commençons par un document vide appelé ``main.qml``. Tous les fichiers QML doivent avoir pour estension ``.qml``. Comme un langage de balisage (comme le HTML), un document QML doit avoir un et un seul élément racine, qui dans notre cas présent est l'élément ``Image`` dont la largeur et la longueur sont fonction des dimensions de l'image d'arrière plan.

.. code-block:: qml

    import QtQuick 2.3

    Image {
        id: root
        source: "images/background.png"
    }

Vu que QML ne fait aucune restriction sur le type d'élément utilisé en tant qu'élément racine, nous utilisons un élément ``Image`` comme élément racine avec la propriété source défini à notre image d'arrière plan.


.. image:: ./../en/ch01/src/showcase/images/background.png


.. note::

    Chaque élément a des propriétés, ex. une image a un ``width``, ``height`` mais qussi d'autres propriétés comme la propriété ``source``. La taille de l'élément image est automatiquement déduite de la taille de l'image. Autrement nous aurions besoin de définir les propriétés ``width`` et ``height`` à une valeur appropriée en pixel.

    Les éléments standard sont dans le module ``QtQuick`` que incluons en premiere ligne avec l'instruction import.

    La propriété spéciale ``id`` est optionnel et contient un identifiant pour référencer l'élement plus tard dans le reste du document. Important: Une propriété ``id`` ne peut plus être modifié une fois qu'il est défini et ne peut pas être défini durant l'exécution. Utiliser ``root`` comme id pour l'élément racine est juste une habitude de l'auteur et rend prévisible le référencement à l'élément racine dans la plus part des documents QML.

Les éléments en premier plan, le mât et la roue à picots, de notre interface utilisateur sont dans des images distinctes.

.. image:: ./../en/ch01/src/showcase/images/pole.png
.. image:: ./../en/ch01/src/showcase/images/pinwheel.png

Le mât sera placé au centre horizontal de l'arrière plan vers le bas. Et la roue à picots pourra être placé au centre de notre arrière plan.

Normalement votre interface utilisateur devra être composée de plusieurs type éléments et non seulement d'éléments image comme c'est le cas dans cet exemple.


.. code-block:: qml

  Image {
      id: root
      ...
      Image {
          id: pole
          anchors.horizontalCenter: parent.horizontalCenter
          anchors.bottom: parent.bottom
          source: "images/pole.png"
      }

      Image {
          id: wheel
          anchors.centerIn: parent
          source: "images/pinwheel.png"
      }
      ...
  }



Pour placer la roue à picot au centre nous utilisons une propriété complexe appelée ``anchor`` (ancrage). L'encrage vous permet de spécifier les relations géométriques entre les objects parents et les objets suivants. Ex. Pour me placer au centre d'un autre élément ( ``anchors.centerIn: parent`` ). Il y existe également les relations left, right, top, bottom, centerIn, fill, verticalCenter and horizontalCenter utilisable aux deux extrémités. Bien entendu ils doivent correspondre. Ancrer mon côté gauche (left) au côté spérieur (top) d'un élément n'a aucun sens.

Ainsi, nous avons centré notre roue à picots au centre de son élément parent, notre arrière plan.

.. note::

    Parfois, vous aurez besoin de faire de petits ajustements au centre exact. Ceci est possible avec ``anchors.horizontalCenterOffset`` ou avec ``anchors.verticalCenterOffset``. Les propriétés d'ajustements similaires sont aussi valables pour les autres ancrages. Consultez la documentation pour la liste complète des propriétés d'ancrage.

.. note::

    Placer une image en tant qu'enfant de notre élément rectangle racine montre un important concept du langage déclaratif. Vous décrivez l'interface utilisateur dans l'ordre des couches et de groupement, où la couche supérieur (notre rectangle) est déssinés en premier et les couches enfants sont déssinées au dessus de celui-ci dans le système de coordonnées local de l'élément qui les contient.

Pour rendre la démo un petit peu plus intéressante, nous aimerions rendre la scène plus interactive. L'idée est de faire tourner la roue lorsque l'utilisateur clique sur la souris n'importe où sur la scène.


Nous utilisons l'élément ``MouseArea`` et le rendons aussi grand que notre élément racine.

.. code-block:: qml

    Image {
        id: root
        ...
        MouseArea {
            anchors.fill: parent
            onClicked: wheel.rotation += 90
        }
        ...
    }

L'élément MouseArea émet un signal lorsque l'utilisateur clique à l'intérieur de la zone qu'il couvre. Vous pouvez détecter ce signal en redéfinissant la fonction ``onClicked``. A cet instant, on référence l'image de la roue et on change la rotation à +90 degree.

.. note::

    Ceci marche pour tous les signaux, le convention de nom est ``on`` + ``NonDuSignal`` avec la première lettre en majuscule. Aussi toutes les propriétés émettent un signal lorsque leur valeur change. la convention de nom est:

        ``on`` + ``NomDeLaPropriete`` + ``Changed``

    Si une propriété ``width`` est modifiée, vous pouvez surveillz la valeur du width pa exemple ``onWidthChanged: print(width)``.

A présent, la roue tournera, mais ce n'est toujours pas aussi fluide. La propriété de rotation change immédiatement. Ce que nous aurions aimé c'est de voir la roue tourner de 90 dégrés au fil du temps. C'est de là qu'entrent en jeu les animations. Une animation définit comment le changement de la valeur d'une propriété est distribué dans le temps. Pour permettre celà, nous type d'animation appelé behavior. ``Behaviour`` ne specify une animation que pour une propriété bien définie et pour chaque changement appliqué à cette propriété. En résumé, chaque fois aue la propriété change, l'animation est lancée. Ceci est seulement une des nombreuses manières pour déclarer une animation en QML.

.. code-block:: qml

    Image {
        id: root
        Image {
            id: wheel
            Behavior on rotation {
                NumberAnimation {
                    duration: 250
                }
            }
        }
    }

A présent, lorsque la rotation de la roue changera, il sera animé en utilisant un ``NumberAnimation`` avec une durée de 250 ms. Donc chaque tour de 90 dégrés durera 250 ms.

.. image:: ./../en/ch01/assets/scene2.png
    :scale: 50%

.. note:: Vous ne verez pas la roue devenir floue. L'image précédente indique juste la rotation. Mais il y a une image d'une roue floue dans le dossier assets. Peut être voudriez vous l'essayer.


La roue ressemble beaucoup mieux à quelque chose à présent. J'espère que ceci vous a donné une petite idée de comment marche la programmation Qt Quick.

Les blocks de fondation de Qt
==============================

Qt 5 se compose d'une grande quantité de modules. Un module est généralement une librairie destinée à l'utilisation d'un développeur. Certains modules sont obligatoires pour faire fonctionner la plateforme Qt. Ils forment un ensemble appelé *Qt Essentials Modules*. De nombreux modules sont optionnels et forment *Qt Add-On Modules*. La majorité des développeurs utilisés par la  des développeurs, mais il est bon de les connaitres car ils fournissent des solutions efficaces à des défis communs.

Modules Qt
---------------------

Les modules Qt Essentials sont necessaires pour faire fonctionner la plateforme Qt. Ils offrent la fondation pour développer une application Qt 5 moderne utilisant Qt Quick 2.

.. rubrique:: Les modules Core-Essential

La liste minimum des modules Qt 5 à connaître pour débuter la programmation QML.

.. list-table::
    :widths: 20 80
    :header-rows: 1

    *   - Module
        - Description
    *   - Qt Core
        - Classes non-graphiques de base utilisées par d'autres modules
    *   - Qt GUI
        - Classes de base pour les composants graphique d'interface utilisateur. Inclue OpenGL.
    *   - Qt Multimedia
        - Classes les fonstionalités audio, video, radio et camera.
    *   - Qt Network
        - Classes pour rendre la programmation réseau facile et portable.
    *   - Qt QML
        - Classes pour les langages QML et JavaScript.
    *   - Qt Quick
        - Framework déclaratif pour conçevoir des applications dynamiques avec des interfaces utilisateur personalisées.
    *   - Qt SQL
        - Classes pour l'intégration de base de données avec SQL.
    *   - Qt Test
        - Classes les tests unitaires des applications et librairies Qt.
    *   - Qt WebKit
        - Classes une implementation de WebKit2 et un nouvel API QML. Voire aussi Qt WebKit Widgets dans les add-on modules.
    *   - Qt WebKit Widgets
        - Classes WebKit1 and QWidget de Qt 4.
    *   - Qt Widgets
        - Classes pour étendre le module Qt GUI aux composants C++.


.. diagraph:: essentials

    QtGui -> QtCore
    QtNetwork ->QtCore
    QtMultimedia ->QtGui
    QtQml -> QtCore
    QtQuick -> QtQml
    QtSql -> QtCore


.. rubric:: Les modules complémentaires de Qt

Outre les modules essentiels, Qt offre des modules additionnels pour les développeurs de logiciels, qui ne font pas partie de la version finale. Voici une petite liste des modules complémentaires.

* Qt 3D - Une liste d'APIs pour la programmation graphique 3D, facile et déclarative.
* Qt Bluetooth - Des APIs C++ et QML pour utiliser la technologie sans file bluetooth
* Qt Contacts - Des APIs C++ et QML pour accéder au carnet d'adresses / aux données des contacts
* Qt Location - Fournit une localisation de la position, la cartographie, la navigation et la recherche de place via des interfaces QML et C++. NMEA backend pour le positionement.
* Qt Organizer - APIs C++ et QML pour accéder aux événements de l'agenda (todos, événments, etc.)
* Qt Publish and Subscribe.
* Qt Sensors - Accès aux capteurs via les interfaces QML et C++.
* Qt Service Framework - Permet aux applications de lire, naviguer et souscrire aux notifications de changement.
* Qt System Info - Accéder aux imformations du système et ses capacités.
* Qt Wayland - Linux seulement. Inclue l'API Qt Compositor (server), et le plugin de Wayland plateforme (clients)
* Qt Feedback - Retour tactile et audio des actions de l'utilisateur.
* Qt JSON DB - Stackage no-SQL d'objet pour Qt.

.. note::

    Comme ces modules ne font pas partie de la version finale, leur état diffère du module et depend selon la façon dont les nombreux contributeurs sont actifs et à quel point le module est testé.

Plateformes supportées
----------------------

Qt supports une variété de plateformes. La majorité des plateformes desktop et embarquées est supportée. Grâce à Qt Application Abstraction, il est facile de nos jours de porter Qt même sur votre propre plateforme si nécessaire.

Tester Qt 5 sur une plateforme prend beaucoup de temps. Quelques unes de ces plateformes ont été sélectionnées par qt-project pour servir de plateformes de référence. Ces plateformes sont testées grâce au système de test pour assurer une meilleure qualité. Rappelez-vous cependant: il n'y a pas de code exempt d'erreurs.




Qt project
==========

Vu sur le `wiki qt-project <http://wiki.qt-project.org>`_:

"Qt-Project est une communauté fondée sur un concensus méritocratique qui s'intéresse à Qt. Quiconque partage cet intérêt peut rejoindre la communauté, participer au processus de décision et contribuer à son développement."

Qt-Project est une organisation qui développe la partie open-source de Qt. Elle construit la base pour permettre à d'autres utilisateurs de contribuer. Le plus grand contributeur est DIGIA, qui détient également les droits commerciaux sur Qt.

Qt a un aspect open-source et un aspect commercial pour les entreprises. L'aspect commercial est pour les entreprises qui ne peuvent pas ou ne veulent pas se conformer aux licences open-source. Sans cet aspect commercial, ces compagnies n'auraient pas été capables d'utiliser Qt et ne permettraient pas à DIGIA de contribuer autant au code de Qt-Project.

Il y a beaucoup de sociétés dans le monde qui gagnent leur vie sur du conseil et le développement de produit utilisant Qt sur différentes plateformes. Il y a plusieurs projets open-source et développeurs open-sources qui utilisent Qt comme leur pricipale librairie de développement. C'est bon de faire partie de cette vibrante communquté et de travailler avec ces merveilleux outils et librairies. Cela fait-il de vous une meilleure personne? Peut-être bien:-)

**Contribuer ici: http://wiki.qt-project.org**
