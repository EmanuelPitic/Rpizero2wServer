
# MQTT5 Broker

Acest proiect implementează un broker MQTT5 simplu care gestionează conexiunile clienților, autentificarea și menținerea conexiunilor printr-un server SQL pentru stocarea datelor clientului. Codul este structurat în mai multe module, fiecare având funcționalități specifice pentru decodificarea și crearea pachetelor MQTT, precum și gestionarea conexiunilor și autentificării.

## Structura Proiectului

### Fișierele Principale

- **`server.py`**: Modulul principal care implementează serverul MQTT5. Gestionează conexiunile clienților, interacțiunea cu aceștia și comunicarea cu baza de date.

- **`mqtt_webapp.py`**: Interfața grafică pentru brokerul MQTT. Permite pornirea și oprirea serverului, precum și monitorizarea conexiunilor, mesajelor și altor informații relevante. Are loc pe 192.168.1.120 in cazul nostru, trebuie schimbat de la caz la caz

- **`sqlServer.py`**: Modulul care gestionează operațiile legate de baza de date, incluzând autentificarea, stocarea și actualizarea informațiilor despre clienți în baza de date SQLite.

- **`decoder.py`**: Implementează clasa `MQTTDecoder`, care este utilizată pentru decodificarea pachetelor MQTT primite de la clienți, cum ar fi `CONNECT`, `PINGREQ` și `DISCONNECT`.

- **`packet_creator.py`**: Conține funcțiile necesare pentru crearea pachetelor MQTT, cum ar fi `CONNACK`, `PINGRESP` și `DISCONNECT`, ce sunt trimise ca răspuns către clienți.

## Cerințe

- Python 3.x
- Biblioteca `socket` (inclusă nativ în Python)
- Biblioteca `struct` (inclusă nativ în Python)

## Configurare Server

Serverul este configurat să ruleze pe adresa IP `192.168.1.120` (localhost) și pe portul `5500`. Aceste valori pot fi modificate în fișierul `server.py`.

## Utilizare

1. **Pornirea Serverului**:
   Pentru a porni serverul MQTT5 Broker folosind interfața grafică, rulează comanda:
   ```bash
   python mqqt_webapp.py
   ```
   Accesati pagina web de la adresa ip: `192.168.1.120`, portul 8082
   Din interfața grafică, apasă butonul **Start Server** pentru a iniția serverul.

2. **Monitorizarea Conexiunilor și Mesajelor**:
   - **Tabul Topic History**: Afișează istoricul topicurilor utilizate.
   - **Tabul Last 10 Messages**: Arată ultimele 10 mesaje publicate pe un topic selectat.
   - **Tabul Connected Clients**: Listează clienții conectați și abonamentele acestora.
   - **Tabul Subscribed Clients**: Prezintă clienții abonați pentru fiecare topic.
   - **Tabul QoS 1/2 Messages**: Afișează mesajele publicate cu QoS 1 și 2.

3. **Oprirea Serverului**:
   Din interfața grafică, apasă butonul **Stop Server** pentru a opri serverul.

## Detalii Despre Module

### server.py

`server.py` este modulul principal care gestionează conexiunile clienților, autentificarea acestora și procesarea pachetelor MQTT folosind `decoder.py` și `packet_creator.py`. 

### mqtt_webapp.py

`mqtt_webapp.py` implementează interfața grafică a brokerului, permițind pornirea și oprirea serverului, precum și vizualizarea și gestionarea datelor într-un mod intuitiv, activa pe portul `192.168.1.120`, in cazul meu.

### sqlServer.py

`sqlServer.py` definește clasa `SQLServer` pentru interacțiunea cu baza de date. Acest modul gestionează autentificarea și păstrarea informațiilor despre clienți, inclusiv ora ultimei deconectări.

### decoder.py

`decoder.py` implementează clasa `MQTTDecoder` pentru decodificarea pachetelor MQTT. Aceasta interpretează pachetele primite de tip `CONNECT`, `PINGREQ` și `DISCONNECT`.

### packet_creator.py

`packet_creator.py` conține funcțiile necesare pentru crearea pachetelor MQTT, inclusiv:
- **`create_connack_packet`**: Creează un pachet de tip `CONNACK` pentru a confirma conexiunea cu clientul.
- **`create_pingresp_packet`**: Creează un pachet `PINGRESP` pentru a menține sesiunea activă.
- **`create_disconnect_packet`**: Creează un pachet `DISCONNECT` pentru a informa clientul că a fost deconectat.


