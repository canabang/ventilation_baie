# 📔 Tutoriel : Mise en place du Système de Ventilation

Ce guide vous accompagne pas à pas dans l'installation et la configuration de votre système de refroidissement intelligent.

## 1. Câblage (ESP32-S3)

Référez-vous aux numéros de broches sur le connecteur de votre ventilateur :

![Câblage ventilateur 4-pins](docs/fan_pinout.png)

| Broche | Fonction | Destination ESP32 / Alim | Note |
| :--- | :--- | :--- | :--- |
| **1** | **Ground (GND)** | **GND** (Commun) | Masse |
| **2** | **VCC (12V)** | **+12V** (Alim externe) | Alimentation |
| **3** | **Signal (Tacho)** | **GPIO4** | Lecture RPM |
| **4** | **PWM** | **GPIO6** | Contrôle vitesse |

> [!CAUTION]
> N'oubliez pas de relier le **GND** de votre alimentation 12V au **GND** de l'ESP32 pour que le signal PWM fonctionne.

## 2. Configuration logicielle

### Préparation des secrets
À la racine du projet, créez un fichier `secrets.yaml` :
```yaml
wifi_ssid: "VOTRE_WIFI"
wifi_password: "VOTRE_MOT_DE_PASSE"
```

### Flashage
Connectez votre ESP32 en USB et lancez la commande suivante :
```bash
esphome run ventilation_v1.yaml
```

## 3. Intégration Home Assistant

Une fois flashé, ESPHome sera automatiquement détecté par Home Assistant.

### Configuration de la Carte (Dashboard)
Pour un contrôle optimal, ajoutez ces éléments à votre tableau de bord :

1.  **Contrôle Auto** : `switch.mode_automatique`
2.  **Réglage Temp Min** : `number.consigne_temp_min` (Définit quand le ventilateur démarre)
3.  **Réglage Temp Max** : `number.consigne_temp_max` (Définit quand il atteint 100%)
4.  **Afficheurs** : 
    - `sensor.vitesse_ventilateur` (RPM)
    - `sensor.puissance_ventilateur` (%)
    - `sensor.temperature_ambiante` (°C)

### 🚀 Mode Boost (Nouveau)
Le bouton **Mode Boost** permet de forcer instantanément tous les ventilateurs à 100% (utile si vous installez un nouveau logiciel ou si la baie chauffe anormalement).
- **Durée Boost** : Réglez le curseur "Durée Boost" (ex: 10 min).
- **Activation** : Actionnez "Mode Boost". Le ventilateur passera à 100% et le switch s'éteindra automatiquement à la fin du décompte.
- **Retour Auto** : À la fin de la durée, le système repasse automatiquement en mode courbe automatique (ou manuel selon l'état précédent).

### Exemple de comportement
Si vous réglez **Min = 25°C** et **Max = 35°C** :
- À **24°C** : Ventilateur **éteint**.
- À **30°C** : Ventilateur à **50%** (milieu de courbe).
- À **36°C** : Ventilateur à **100%**.

## 🧠 Astuces

- **Mode Manuel** : Dès que vous bougez le curseur de vitesse manuelle, le mode automatique se désactive pour vous laisser la main.
- **Vérification** : Consultez les logs ESPHome pour voir la ligne `Mode AUTO - Température: XX°C -> Ventilateur: XX%` s'afficher toutes les 30 secondes.
