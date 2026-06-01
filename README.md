# Lab-21-Capteurs-embarqu-s-Android
# Application Android Capteurs Embarqués

Application Android complète permettant d'exploiter tous les capteurs embarqués d'un smartphone : affichage des capteurs disponibles, visualisation des mesures en temps réel sous forme de graphes, boussole numérique, compteur de pas et reconnaissance simple d'activité.

## Table des matières

- [Description générale](#description-générale)
- [Objectifs pédagogiques](#objectifs-pédagogiques)
- [Architecture du projet](#architecture-du-projet)
- [Capteurs supportés](#capteurs-supportés)
- [Technologies utilisées](#technologies-utilisées)
- [Prérequis](#prérequis)
- [Structure du projet](#structure-du-projet)
- [Installation](#installation)
- [Partie 1 : Configuration du projet](#partie-1--configuration-du-projet)
- [Partie 2 : Affichage des capteurs disponibles](#partie-2--affichage-des-capteurs-disponibles)
- [Partie 3 : Vue de graphe personnalisée](#partie-3--vue-de-graphe-personnalisée)
- [Partie 4 : Capteurs environnementaux](#partie-4--capteurs-environnementaux)
- [Partie 5 : Capteurs de mouvement](#partie-5--capteurs-de-mouvement)
- [Partie 6 : Compteur de pas](#partie-6--compteur-de-pas)
- [Partie 7 : Boussole numérique](#partie-7--boussole-numérique)
- [Partie 8 : Reconnaissance d'activité](#partie-8--reconnaissance-dactivité)
- [Partie 9 : Intégration finale](#partie-9--intégration-finale)
- [Test avec l'émulateur](#test-avec-lémulateur)
- [Bonnes pratiques](#bonnes-pratiques)
- [Dépannage](#dépannage)

## Description générale

Cette application permet de :

1. **Lister tous les capteurs** disponibles sur le téléphone avec leurs caractéristiques techniques
2. **Visualiser les mesures** en temps réel sous forme de graphes
3. **Exploiter les capteurs environnementaux** : température, humidité, proximité, champ magnétique
4. **Exploiter les capteurs de mouvement** : accéléromètre, gravité, gyroscope
5. **Compter les pas** avec économie d'énergie
6. **Afficher une boussole numérique** indiquant la direction
7. **Reconnaître l'activité** de l'utilisateur (marche, saut, stable, assis/debout)

## Objectifs pédagogiques

À la fin de ce TP, vous serez capable de :

| Compétence | Description |
|------------|-------------|
| **SensorManager** | Comprendre le rôle du gestionnaire de capteurs Android |
| **Lister les capteurs** | Afficher tous les capteurs disponibles avec leurs propriétés |
| **SensorEventListener** | Écouter et recevoir les mesures des capteurs en temps réel |
| **Graphes personnalisés** | Créer une vue personnalisée pour visualiser l'évolution des données |
| **Accéléromètre/Gyroscope** | Exploiter les capteurs de mouvement pour analyser l'orientation |
| **Compteur de pas** | Utiliser TYPE_STEP_COUNTER avec la permission ACTIVITY_RECOGNITION |
| **Boussole** | Combiner accéléromètre et magnétomètre pour obtenir l'orientation |
| **Reconnaissance d'activité** | Analyser les données pour détecter marche, saut, position stable |
| **Économie d'énergie** | Désactiver les capteurs dans onPause() pour préserver la batterie |

## Architecture du projet

## Capteurs supportés

| Capteur | Type Android | Affichage |
|---------|--------------|-----------|
| Température ambiante | `TYPE_AMBIENT_TEMPERATURE` | Graphe simple |
| Humidité relative | `TYPE_RELATIVE_HUMIDITY` | Graphe simple |
| Proximité | `TYPE_PROXIMITY` | Graphe simple |
| Champ magnétique | `TYPE_MAGNETIC_FIELD` | Graphe (norme x,y,z) |
| Accéléromètre | `TYPE_ACCELEROMETER` | 3 axes + norme |
| Gravité | `TYPE_GRAVITY` | 3 axes + norme |
| Gyroscope | `TYPE_GYROSCOPE` | 3 axes + norme |
| Compteur de pas | `TYPE_STEP_COUNTER` | Nombre de pas |
| Boussole | Combinaison | Direction en degrés |

## Technologies utilisées

| Composant | Technologie | Version |
|-----------|-------------|---------|
| Langage | Java | 1.8 |
| Capteurs | Android Sensor Framework | API 24+ |
| UI | Fragments, Navigation Drawer | - |
| Graphique | Vue personnalisée (Canvas) | - |
| Permissions | ACTIVITY_RECOGNITION (Android Q+) | - |

## Prérequis

- Android Studio Hedgehog ou supérieur
- JDK 11 ou supérieur
- SDK Android API 24 minimum
- **Téléphone physique** recommandé (certains capteurs ne sont pas sur émulateur)
- Ou émulateur avec Virtual Sensors activés

## Structure du projet

## Installation

### 1. Créer le projet

```bash
Android Studio > File > New > New Project > Empty Activity
Nom : Sensors
Language : Java
Minimum SDK : API 24
Package name : com.example.sensors
Finish<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android">

    <!-- Permission pour le compteur de pas (Android Q+) -->
    <uses-permission android:name="android.permission.ACTIVITY_RECOGNITION" />

    <application
        android:allowBackup="true"
        android:icon="@mipmap/ic_launcher"
        android:label="Capteurs"
        android:theme="@style/Theme.Sensors">
        
        <activity
            android:name=".MainActivity"
            android:exported="true">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />
                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
        
    </application>

</manifest>Clic droit sur le package principal > New > Package
- fragments
- utils
- views
