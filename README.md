https://plainenglish.io/blog/making-a-synth-with-python-oscillators-2cb8e68e9c3b<br>
https://github.com/mdoege/PySynth<br>
https://github.com/dayunbao/supriya_demos/blob/main/midi_synth/midi_synth.py<br>
-Play a sound wave (sine, saw, square, trangle, etc...)
Créer un synthétiseur en Python est un projet passionnant et il existe plusieurs bibliothèques qui peuvent t'aider à implémenter cela. Voici les étapes de base et les bibliothèques recommandées pour réaliser ton synthétiseur.

### Bibliothèques recommandées

1. **Pydub** : Utilisé pour la manipulation audio, y compris la création de sons, la modification de fréquence, de volume, et le mixage.
   
   Installation :
   ```bash
   pip install pydub
   ```

2. **NumPy** : Une bibliothèque essentielle pour la manipulation de tableaux numériques, utilisée ici pour générer des ondes sonores à des fréquences spécifiques.

   Installation :
   ```bash
   pip install numpy
   ```

3. **Sounddevice** : Permet de jouer des sons générés dans Python directement via la carte son de l'ordinateur.

   Installation :
   ```bash
   pip install sounddevice
   ```

4. **Scipy** (facultatif) : Si tu souhaites utiliser des fonctions avancées pour la génération d'ondes et des effets sonores complexes.

   Installation :
   ```bash
   pip install scipy
   ```

### Étapes de base pour créer un synthétiseur

1. **Générer des ondes sonores** : Un synthétiseur produit des sons en générant des ondes de différentes formes, comme des ondes sinusoïdales, carrées, triangulaires, etc. Tu peux utiliser NumPy pour créer des tableaux qui représentent ces ondes.

2. **Jouer les sons** : Après avoir généré une onde, tu peux utiliser `sounddevice` pour la lire.

3. **Moduler la fréquence** : Pour simuler différentes notes musicales, tu peux ajuster la fréquence de l'onde sinusoïdale.

### Exemple simple de synthétiseur

Voici un exemple très simple d'un synthétiseur qui génère un son sinusoidal (une note de base) et la joue avec une fréquence ajustable.

```python
import numpy as np
import sounddevice as sd

# Paramètres du son
rate = 44100  # Fréquence d'échantillonnage (samples par seconde)
duration = 1  # Durée du son en secondes
frequency = 440  # Fréquence de la note (A4, 440 Hz)

# Générer une onde sinusoïdale
t = np.linspace(0, duration, int(rate * duration), endpoint=False)  # Générer le temps
wave = 0.5 * np.sin(2 * np.pi * frequency * t)  # Générer une onde sinusoïdale

# Jouer le son
sd.play(wave, rate)
sd.wait()  # Attendre que la lecture soit terminée
```

### Explications :

- **NumPy** est utilisé pour créer une onde sinusoïdale à une fréquence donnée.
- **Sounddevice** est utilisé pour jouer l'onde générée sur la carte son.

### Ajouter des fonctionnalités supplémentaires :

1. **Changer de forme d'onde** : Tu peux remplacer la fonction sinusoïdale par des formes d'onde carrées, triangulaires ou en dents de scie pour des sons différents.

   Exemple pour une onde carrée :
   ```python
   wave = 0.5 * np.sign(np.sin(2 * np.pi * frequency * t))  # Onde carrée
   ```

2. **Générer des accords** : Pour jouer plusieurs notes simultanément, tu peux ajouter plusieurs ondes de fréquences différentes.

   Exemple d'accord :
   ```python
   frequencies = [440, 554, 659]  # Notes A4, C#5, E5
   wave = sum(0.5 * np.sin(2 * np.pi * f * t) for f in frequencies)
   ```

3. **Synthèse d'enveloppe (ADS)** : Pour modifier la façon dont le son évolue dans le temps (attaque, déclin, sustain, release), tu peux implémenter une enveloppe ADSR. Cela modifie le volume du son en fonction du temps.

   Exemple simplifié d'une enveloppe :
   ```python
   attack_time = 0.1  # Temps d'attaque en secondes
   release_time = 0.2  # Temps de relâchement en secondes

   envelope = np.concatenate([
       np.linspace(0, 1, int(rate * attack_time)),  # Attaque
       np.ones(int(rate * (duration - attack_time - release_time))),  # Sustain
       np.linspace(1, 0, int(rate * release_time))  # Release
   ])

   wave *= envelope[:len(wave)]  # Appliquer l'enveloppe
   ```

### Pour aller plus loin :
- **Ajouter des effets** : Tu peux ajouter des effets comme la réverbération, le chorus, ou le delay en manipulant les signaux audio.
- **Interface graphique** : Si tu veux ajouter une interface utilisateur pour contrôler ton synthétiseur, tu peux utiliser des bibliothèques comme **Tkinter** ou **PyQt**.
- **Simulation d'instruments** : Avec des techniques avancées, tu peux simuler des instruments spécifiques comme des pianos, des guitares ou des percussions.

Avec ces bases, tu peux déjà créer un synthétiseur fonctionnel. Si tu veux un projet plus complexe, comme une interface complète ou des sons plus sophistiqués, n'hésite pas à poser des questions supplémentaires !
