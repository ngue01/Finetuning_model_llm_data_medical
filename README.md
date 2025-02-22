# 🧠 Fine-Tuning Large Language Models (LLMs) with LoRA and Quantization

## Introduction

Ce projet consiste à **fine-tuner un modèle de langage** (LLM) en utilisant des techniques de **quantization** et **Low-Rank Adaptation (LoRA)**. L'objectif est de rendre l'entraînement plus efficace, en optimisant la consommation de mémoire et les performances, tout en maintenant un haut niveau de précision pour des tâches telles que la génération de texte basée sur un modèle causal.

Le projet utilise **Hugging Face Transformers**, **LoRA**, et **PyTorch** pour fine-tuner un modèle pré-entraîné sur des données médicales.

---

## Objectifs

Les objectifs principaux du projet sont :
1. Fine-tuner un modèle de langage (**phi-2** de Microsoft) sur un dataset médical pour améliorer sa précision.
2. Optimiser l'entraînement avec la **quantization** 4 bits et l'adaptation LoRA, permettant un entraînement efficace avec moins de ressources.
3. Enregistrer le modèle fine-tuné pour un usage futur ou une évaluation sur d'autres tâches.

---

## Caractéristiques Clés

1. **Quantization 4-bits** : Le modèle est quantifié à 4 bits pour réduire la consommation mémoire et accélérer l'entraînement.
2. **Low-Rank Adaptation (LoRA)** : Une technique utilisée pour ajuster les couches spécifiques du modèle, permettant un fine-tuning rapide avec des ressources limitées.
3. **Dataset Médical** : Le modèle est fine-tuné sur un dataset spécifique au domaine médical, ce qui permet d'améliorer sa capacité à répondre à des questions dans ce domaine.
4. **Sauvegarde du modèle** : Après l'entraînement, le modèle est sauvegardé pour des usages futurs.

---

## Approche Technique

### 1. **Préparation des Données**
   - Le dataset utilisé est [MedQuad-phi2-1k](https://huggingface.co/datasets/prsdm/MedQuad-phi2-1k)   de Hugging Face, un dataset médical.
   - Les données sont formatées avec des templates de prompt (avec ou sans input) pour préparer les entrées du modèle.

### 2. **Quantization Configuration**
   - Le modèle est configuré pour être chargé en **4-bit** à l'aide de la bibliothèque `BitsAndBytesConfig`.
   - Cela permet de réduire l'utilisation de la mémoire tout en maintenant les performances lors de l'entraînement.

### 3. **Low-Rank Adaptation (LoRA)**
   - LoRA est configuré pour ajuster les couches spécifiques du modèle. Cette technique permet un fine-tuning rapide sans ajuster tous les paramètres du modèle, ce qui réduit encore la charge computationnelle.

### 4. **Entraînement**
   - Le modèle est fine-tuné avec des hyperparamètres optimisés pour un entraînement efficace. Les étapes d'entraînement incluent la configuration des taux d'apprentissage, le contrôle de gradient et le décrochage.

### 5. **Sauvegarde et Export**
   - Le modèle fine-tuné est enregistré sous le nom `phi-2-1a-kevin` pour être utilisé ou évalué dans des tâches futures.

---

## Technologies Utilisées

- **Python** : Le langage principal utilisé pour ce projet.
- **Hugging Face Transformers** : Utilisé pour charger, entraîner, et évaluer le modèle de langage.
  - [Hugging Face Transformers Documentation](https://huggingface.co/transformers/)
- **LoRA (Low-Rank Adaptation)** : Utilisé pour ajuster le modèle de manière efficace.
  - [LoRA Documentation](https://github.com/microsoft/LoRA)
- **PyTorch** : Utilisé pour l'entraînement et l'évaluation du modèle.
  - [PyTorch Documentation](https://pytorch.org/)
- **BitsAndBytes** : Permet la quantization du modèle pour une utilisation plus efficace de la mémoire.
  - [BitsAndBytes Documentation](https://github.com/TimDettmers/bitsandbytes)
- **WandB** : Utilisé pour le suivi et la journalisation des expériences d'entraînement.

---

## Méthodologie et Techniques

### 1. **Formatage des Données**
   - Les données du dataset médical sont formatées avec deux templates : un avec un input contextuel et l'autre sans input, selon la structure des données.

### 2. **Quantization**
   - Le modèle est configuré en **4-bit** via la bibliothèque **BitsAndBytes**, permettant un fine-tuning avec des ressources réduites tout en préservant la précision du modèle.

### 3. **LoRA**
   - LoRA permet de n'ajuster que certaines couches du modèle. Les modules cibles incluent des couches comme `q_proj`, `k_proj`, `v_proj`, et autres modules critiques pour la tâche de génération de texte causal.

### 4. **Entraînement**
   - Le modèle est entraîné avec des hyperparamètres spécifiques, incluant un taux d'apprentissage de `2e-4`, un nombre d'époques fixé à 1, et une accumulation de gradient.

### 5. **Sauvegarde du Modèle**
   - Après l'entraînement, le modèle est sauvegardé pour un déploiement ou une évaluation ultérieure. Le modèle final est enregistré sous le nom `phi-2-1a-kevin`.

---

## Déploiement du Projet
- Vous pouvez télécharger le fichier `fine_tunning.ipynb` et l'exécuter dans un environnement Colab en utilisant un kernel GPU. Assurez-vous d'avoir un compte **Hugging Face** et **Weights & Biases (WandB)** pour suivre les expérimentations et accéder aux modèles et datasets nécessaires.
