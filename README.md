# 🌬️ Ventilation Baie de Brassage (V2 - Dual Zone)

Projet de gestion intelligente de ventilation pour baie de brassage, basé sur **ESPHome** et **Home Assistant**.
Cette version V2 introduit une gestion bi-zone (Haut/Bas) indépendante pour optimiser le flux d'air et le refroidissement.

---

## ✨ Fonctionnalités Principales

*   **⚡ Dual Zone (Haut / Bas)** : Pilotage indépendant de deux rangées de ventilateurs.
*   **🌡️ Mode Automatique Intelligent** :
    *   Régulation PID simplifiée (courbe linéaire) basée sur la température de chaque zone.
    *   **Kickstart** : Impulsion de démarrage pour assurer la rotation des ventilateurs à basse vitesse.
*   **🚀 Mode Boost Global** : "Tout à fond" pendant une durée configurable (ex: 10 min) en un clic.
*   **🛡️ Sécurités Actives (Fail-Safe)** :
    *   **Perte de Sonde** : Si un capteur ne répond plus, la ligne concernée passe à 50% par sécurité.
    *   **Interlock Surchauffe** : Si la T° dépasse le seuil critique (`Max + 5°C`), toutes les lignes passent à 100%.
    *   **Indicateur RPM** : Surveillance de la vitesse réelle des ventilateurs.

---

## 📂 Structure du Projet

*   **`ventilation_v2.yaml`** : Configuration principale ESPHome (Code source à flasher).
*   **`.base.yaml`** : Configuration commune (WiFi, API, OTA).
*   **`ventilation_card.yaml`** : Code YAML complet pour le dashboard Home Assistant (Templates + Vue).
*   **`TUTORIAL.md`** : Guide pas à pas pour le câblage et l'installation.

---

## 🚀 Installation Rapide

1.  **Câblage** : Suivez le guide [TUTORIAL.md](./TUTORIAL.md).
2.  **Flashage** : Copiez les fichiers YAML dans votre dossier ESPHome et flashez votre ESP32.
3.  **Dashboard** : Copiez le contenu de `ventilation_card.yaml` dans une vue "Sections" de votre Home Assistant.

---

## 🔧 Configuration par défaut

*   **Consigne Min** : 25°C (0% de vitesse)
*   **Consigne Max** : 35°C (100% de vitesse)
*   **Durée Boost** : 10 minutes

*Ces valeurs sont ajustables directement depuis le dashboard.*

> [!NOTE]
> **Seuil PWM**: Les ventilateurs ne tournent pas en dessous de **5% de puissance** en raison des caractéristiques techniques des moteurs PWM. C'est un comportement normal du matériel.

---

## 📊 Capteurs et Entités Disponibles

Le système expose les entités suivantes vers Home Assistant :

### **🌡️ Capteurs de Température**
| Entité | Description |
|--------|-------------|
| `sensor.esp_fan_temperature_ligne_1` | Température zone haute (DHT22) |
| `sensor.esp_fan_temperature_ligne_2` | Température zone basse (DHT22) |

### **💨 Capteurs de Vitesse**
| Entité | Description |
|--------|-------------|
| `sensor.esp_fan_vitesse_ligne_1` | Vitesse réelle en RPM (Ligne 1) |
| `sensor.esp_fan_vitesse_ligne_2` | Vitesse réelle en RPM (Ligne 2) |

### **⚡ Capteurs de Puissance**
| Entité | Description |
|--------|-------------|
| `sensor.esp_fan_puissance_ventilateur_l1` | Puissance commandée en % (Ligne 1) |
| `sensor.esp_fan_puissance_ventilateur_l2` | Puissance commandée en % (Ligne 2) |

### **🌀 Contrôles Ventilateurs**
| Entité | Description |
|--------|-------------|
| `fan.esp_fan_ventilateurs_ligne_1` | Contrôle ON/OFF + Vitesse (0-100%) Ligne 1 |
| `fan.esp_fan_ventilateurs_ligne_2` | Contrôle ON/OFF + Vitesse (0-100%) Ligne 2 |

### **🔘 Switches (Modes)**
| Entité | Description |
|--------|-------------|
| `switch.esp_fan_mode_boost` | Active le mode Boost global (100% toutes lignes) |
| `switch.esp_fan_mode_auto_ligne_1` | Active/Désactive mode Auto température L1 |
| `switch.esp_fan_mode_auto_ligne_2` | Active/Désactive mode Auto température L2 |

### **🔢 Réglages Numériques**
| Entité | Description | Plage |
|--------|-------------|-------|
| `number.esp_fan_consigne_temp_min` | Température minimum (0% vitesse) | 20-30°C |
| `number.esp_fan_consigne_temp_max` | Température maximum (100% vitesse) | 25-40°C |
| `number.esp_fan_duree_boost` | Durée du mode Boost | 1-60 min |

### **🚨 Alertes Sécurité**
| Entité | Description |
|--------|-------------|
| `binary_sensor.esp_fan_alerte_capteur_l1` | Capteur DHT défaillant sur Ligne 1 |
| `binary_sensor.esp_fan_alerte_capteur_l2` | Capteur DHT défaillant sur Ligne 2 |
| `binary_sensor.esp_fan_alerte_surchauffe_interlock` | Température critique dépassée (Interlock activé) |

---

## 📖 Documentation Complète

Consultez le [TUTORIAL.md](./TUTORIAL.md) pour le guide complet de câblage et d'installation.
