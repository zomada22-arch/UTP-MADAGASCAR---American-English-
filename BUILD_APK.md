# Générer UTP_MADAGASCAR_American_English_Course.apk

## Méthode la plus simple : Android Studio

1. Installer une version récente d'Android Studio.
2. Ouvrir Android Studio.
3. Choisir **Open**.
4. Sélectionner le dossier `UTP_MADAGASCAR_American_English_Course`.
5. Laisser Android Studio télécharger/synchroniser Gradle et Android SDK.
6. Si demandé, installer Android SDK Platform 35 et Build Tools proposés par Android Studio.
7. Attendre `Gradle sync finished`.
8. Menu **Build → Build App Bundle(s) / APK(s) → Build APK(s)**.
9. L'APK debug sera normalement créé dans :
   `app/build/outputs/apk/debug/app-debug.apk`
10. Renommer une copie en :
   `UTP_MADAGASCAR_American_English_Course.apk`

## Installer sur un téléphone

1. Copier l'APK sur le téléphone Android.
2. Ouvrir le fichier APK.
3. Android peut demander d'autoriser l'installation depuis cette source.
4. Autoriser uniquement la source que vous utilisez pour ce fichier.
5. Installer.
6. Au premier enregistrement vocal, accepter l'autorisation Microphone.

## Pour une APK release signée

Dans Android Studio :

**Build → Generate Signed App Bundle or APK → APK**

Créer/conserver votre keystore UTP en lieu sûr. Ne publiez jamais la clé privée.

## Pourquoi l'APK n'est pas compilé dans le paquet fourni ici

L'environnement de génération actuel ne contient ni Android SDK ni Gradle Android configuré, et l'accès réseau système requis pour les télécharger n'est pas disponible. Le projet source a donc été préparé pour compilation directe dans Android Studio.


## Option GitHub Actions (sans Android Studio local)

Le projet contient déjà `.github/workflows/android-build.yml`.

1. Créer un dépôt GitHub.
2. Envoyer tout le dossier du projet dans le dépôt.
3. Ouvrir l'onglet **Actions**.
4. Lancer **Build Android APK** avec **Run workflow**.
5. À la fin, télécharger l'artifact `UTP-Madagascar-American-English-Course`.
6. Il contient `UTP_MADAGASCAR_American_English_Course.apk`.

Cette méthode construit l'APK dans un environnement Android distant et évite d'installer Android Studio sur le PC.
