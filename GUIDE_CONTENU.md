# Modifier le cours sans refaire l'application

Le fichier principal est :

`app/src/main/assets/course_content.json`

La logique Android est séparée de ce fichier.

## 1. Remplacer le logo

Remplacer :

`app/src/main/res/drawable/utp_logo.jpg`

par le nouveau fichier officiel portant exactement le même nom.

Puis reconstruire l'APK.

## 2. Ajouter un topic

Dans `levels[0].topics`, ajouter par exemple :

```json
{
  "id": "introducing-yourself",
  "title": "Introducing Yourself",
  "available": true,
  "objective": "Introduce yourself naturally in American English.",
  "vocabulary": [],
  "dialogues": [],
  "conversation": [],
  "fastSpeech": []
}
```

Le prototype affiche déjà les 20 futurs topics. Pour activer un topic, mettre `available` à `true` et remplir ses sections. Le même moteur générique ouvrira Vocabulary, Dialogue, Listening/Speaking, Conversation et Test à partir du JSON.

## 3. Ajouter un dialogue

Dans `greetings.dialogues`, copier un objet existant :

```json
{
  "id": "g6",
  "title": "Dialogue 6 – Example",
  "prompt": "How are things?",
  "audioAsset": "",
  "acceptedAnswers": [
    "Things are good.",
    "Pretty good, thanks."
  ],
  "openResponse": false
}
```

## 4. Ajouter une question

Dans ce prototype, une question parlée est un `prompt` de dialogue ou de conversation.

Exemple :

```json
"prompt": "What is your name?"
```

## 5. Ajouter une réponse acceptable

Ajouter simplement une phrase dans `acceptedAnswers` :

```json
"acceptedAnswers": [
  "I'm good.",
  "I'm fine.",
  "I'm doing well."
]
```

L'évaluateur choisit automatiquement la réponse acceptable la plus proche du texte reconnu.

## 6. Réponse ouverte

Pour une question comme `Where are you from?`, il n'est pas logique de prévoir toutes les villes/pays.

Utiliser :

```json
"acceptedAnswers": [],
"openResponse": true,
"minWords": 2
```

Le prototype vérifie alors que la réponse est reconnue et contient un minimum de mots. Une future version avec modèle sémantique pourrait analyser le sens plus finement.

## 7. Ajouter un fichier audio

Copier votre audio dans :

`app/src/main/assets/audio/`

Exemple :

`app/src/main/assets/audio/greeting_hi_how_are_you.mp3`

Puis dans le dialogue :

```json
"audioAsset": "greeting_hi_how_are_you.mp3"
```

Si `audioAsset` est vide, l'application utilise Android TextToSpeech en `en-US`.

## 8. Modifier les scores

La formule est dans :

`SpeechEvaluationEngine.java`

Méthode :

`calculate(...)`

Prototype actuel :

- Pronunciation = 60% confiance reconnaissance + 40% Word Accuracy
- Fluency = rythme estimé par durée + 25% Word Accuracy
- Speaking = 35% Pronunciation + 35% Word Accuracy + 30% Fluency
- Overall = 30% Pronunciation + 30% Word Accuracy + 20% Fluency + 20% Speaking

Modifier les coefficients seulement si leur somme reste cohérente.

## 9. Ajouter un nouveau niveau

Ajouter un nouvel objet dans le tableau `levels` de `course_content.json` :

```json
{
  "id": "level2",
  "title": "LEVEL 2",
  "subtitle": "Intermediate",
  "topics": []
}
```

Le sélecteur de niveaux lit déjà le tableau `levels` dynamiquement. Un nouveau niveau utilisant la même structure de topics apparaîtra dans **Select Level** après reconstruction de l’APK.

## 10. Ajouter du vocabulaire

```json
{
  "word": "How's it going?",
  "meaning": "Comment ça va ?",
  "example": "Hey! How's it going?"
}
```

## Structure pédagogique recommandée par topic

`Vocabulary → Dialogue → Listening → Speaking → Evaluation → Score → Feedback`
