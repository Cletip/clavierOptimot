# Installation de la couche basique

Deux manières de l'installer : 

## Directement sur Ubuntu, avec les droits d'administrateur 
### Fichier symboles
Avec les privilèges sudo, ajoutez la section xkb suivante à la fin du fichier `/usr/share/X11/xkb/symbols/fr`
```c
partial alphanumeric_keys
xkb_symbols "optimot_ergo" {
    ...
};
```
### Fichiers lst
Ensuite, dans `/usr/share/X11/xkb/rules/base.lst`, nous devons ajouter
```lst
optimot_ergo    fr: French (Optimot, clavier Ergo)
```
après la section `!variant`.
La même chose doit être faite dans `/usr/share/X11/xkb/rules/evdev.lst`

### Fichiers xml
Ensuite dans `/usr/share/X11/xkb/rules/base.xml` la section suivante doit être ajoutée dans la `variantlist` du `layout` "fr"
```xml
        <variant>
          <configItem>
            <name>optimot_ergo</name>
            <description>French (Optimot, clavier Ergo)</description>
          </configItem>
        </variant>
```
La même chose doit être faite dans `/usr/share/X11/xkb/rules/evdev.xml`

## Depuis la console, mais de manière temporaire et sans les droits d'administrateur
Pour enregistrer le xkb depuis la console et l'utiliser sur la session en cours :
```bash
$ xkbcomp -w0 Optimot.xkb $DISPLAY
```
Ensuite, la disposition du clavier devrait être disponible.


# Installation des couches composée : 

1. Le fichier de contenu XCompose peut être ajouté dans `/usr/share/X11/locale/en_US.UTF-8/Compose`.
   Mais le moyen le plus pratique de l'utiliser consiste à copier le fichier de composition tel qu'il se trouve dans le répertoire d'accueil de l'utilisateur sous le nom `.XCompose` :
   ```bash
   $ cp ./XCompose ~/.XCompose 
   ```

2. Une fois terminé lancez :
   ```bash
   $ sudo dpkg-reconfigure xkb-data
	```
	et redémarrer la machine


## Crédits
Merci à @TrucTruc pour l'aide sur ces instructions
