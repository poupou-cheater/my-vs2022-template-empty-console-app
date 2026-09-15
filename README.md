# Template Visual Studio 2022 : Empty Console Project

Modèle de projet C++ console personnalisé pour **Visual Studio 2022**, optimisé avec les standards modernes et une arborescence standardisée.

---

## 📋 Caractéristiques du Projet

- **Normes du langage** :
  - **C++20** (`<LanguageStandard>stdcpp20</LanguageStandard>`)
  - **C17** (`<LanguageStandard_C>stdc17</LanguageStandard_C>`)
- **Dossiers d'Inclusions (`AdditionalIncludeDirectories`)** :
  - `$(ProjectDir)include` (vos headers)
  - `$(ProjectDir)ext` (vos bibliothèques tierces / externes)
- **Sorties de compilation (`OutDir` / `IntDir`)** :
  - `bin\$(Platform)\$(Configuration)\` : exécutables et dll finaux
  - `obj\$(Platform)\$(Configuration)\` : fichiers objets temporaires (.obj, .pdb, etc.)
- **Point d'entrée & Structure** :
  - `src\main.cpp` (avec `#include "main.h"`)
  - `include\main.h` (Header principal avec `#pragma once`)
  - `ext\readme.txt` (Dossier pour les dépendances externes)
  - `asset\readme.txt` (Dossier pour les assets et ressources)
  - `.gitignore` (Déployé sur disque, invisible dans l'Explorateur de solutions VS)

---

## 📦 Fichiers composant le Template ZIP

L'archive ZIP (`EmptyConsoleProject.zip`) contient **directement à sa racine** :

```text
EmptyConsoleProject.zip
├── $projectname$.vcxproj          (Configuration MSBuild C++20, C17, bin/obj, include/ext)
├── $projectname$.vcxproj.filters  (Filtres virtuels : src, include, ext, asset)
├── .gitignore                     (Fichier gitignore déployé sur le disque)
├── main.cpp                       (Extrait dans src/main.cpp)
├── main.h                         (Extrait dans include/main.h)
├── ext_readme.txt                 (Extrait dans ext/readme.txt)
├── asset_readme.txt               (Extrait dans asset/readme.txt)
├── MyTemplate.vstemplate          (Manifeste du modèle VS)
└── __TemplateIcon.jpg             (Icône personnalisée affichée dans VS)
```

---

## 🛠️ Comment créer le fichier ZIP soi-même

### Méthode 1 : Manuellement (Explorateur Windows / 7-Zip)

1. Placez les fichiers nécessaires dans un dossier de travail :
   - `$projectname$.vcxproj`
   - `$projectname$.vcxproj.filters`
   - `.gitignore`
   - `main.cpp`
   - `main.h`
   - `ext_readme.txt`
   - `asset_readme.txt`
   - `MyTemplate.vstemplate`
   - `__TemplateIcon.jpg`
2. Sélectionnez l'ensemble des fichiers (et non pas le dossier parent).
3. Clic droit $\rightarrow$ **Compresser dans un fichier ZIP** (ou via 7-Zip).
4. Renommez l'archive : `EmptyConsoleProject.zip`.

> [!WARNING]
> Les fichiers doivent impérativement se trouver **à la racine du ZIP**. Si le ZIP contient un sous-dossier contenant les fichiers, Visual Studio ne trouvera pas le manifeste `.vstemplate`.

---

### Méthode 2 : Par script Python automatique

```python
import os
import zipfile
import shutil

build_dir = "temp_build"
os.makedirs(build_dir, exist_ok=True)

# Copier les fichiers du template dans build_dir

output_zip = "EmptyConsoleProject.zip"
with zipfile.ZipFile(output_zip, "w", zipfile.ZIP_DEFLATED) as zipf:
    for root, dirs, files in os.walk(build_dir):
        for file in files:
            full_path = os.path.join(root, file)
            rel_path = os.path.relpath(full_path, build_dir)
            zipf.write(full_path, rel_path)

shutil.rmtree(build_dir, ignore_errors=True)
print("ZIP généré avec succès !")
```

---

## 🚀 Comment installer le Template dans Visual Studio 2022

### Étape 1 : Copier le fichier ZIP

Copiez `EmptyConsoleProject.zip` dans votre répertoire de modèles utilisateur Visual Studio :

```text
C:\Users\<VotreNomUtilisateur>\Documents\Visual Studio 2022\Templates\ProjectTemplates\Visual C++\
```

*(Si le sous-dossier `Visual C++` n'existe pas, créez-le).*

---

### Étape 2 : Vider le cache de Visual Studio (Recommandé lors d'une mise à jour)

1. Fermez Visual Studio.
2. Supprimez les caches :
   - `%USERPROFILE%\AppData\Roaming\Microsoft\VisualStudio\17.0_*\ProjectTemplatesCache`
   - `%USERPROFILE%\AppData\Local\Temp\VsTempFiles`
3. Rouvrez Visual Studio 2022.

---

## 💻 Utilisation dans Visual Studio 2022

1. Lancez **Visual Studio 2022**.
2. Cliquez sur **Créer un projet**.
3. Dans la liste (filtre langage : **C++**), sélectionnez **Empty Console Project** (*made by poupou*).
4. Choisissez le nom et l'emplacement de votre projet, puis validez.
5. Votre projet est immédiatement opérationnel :
   - C++20 & C17 activés
   - Sorties `bin/` et `obj/` configurées
   - `src/main.cpp` et `include/main.h` prêts
   - `ext/` et `asset/` disponibles
