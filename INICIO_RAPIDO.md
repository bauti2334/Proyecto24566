# ⚡ INICIO RÁPIDO — ProyectoNodo IoT

## Firebase ya configurado ✓
- URL: https://proyectonodo-default-rtdb.firebaseio.com
- Clave: serviceAccountKey.json (incluida)

---

## PASO 1 — Instalar Node.js
Descargar de https://nodejs.org (versión LTS)

---

## PASO 2 — Instalar dependencias del backend

Abrir terminal en la carpeta `backend/` y correr:

```
npm install
```

---

## PASO 3 — Cargar datos iniciales en Firebase (UNA SOLA VEZ)

```
node init-db.js
```

Esto crea en tu base de datos:
- 4 sectores (Planta Norte, Sur, Oficinas, Almacén)
- 4 usuarios (admin/1234, carlos/mod123, sofia/mod456, juan/cli123)
- Umbrales por defecto

---

## PASO 4 — Iniciar el backend

```
node server.js
```

---

## PASO 5 — Abrir el dashboard

Abrir en el navegador: http://localhost:3000

Usuario: admin
Contraseña: 1234

---

## PASO 6 — Probar sin hardware ESP32 (opcional)

Abrir otra terminal en `backend/` y correr:

```
node simulador.js
```

Esto simula 10 sensores enviando datos cada 8 segundos.
Ir al dashboard → Descubrimiento → van a aparecer los sensores.

---

## PASO 7 — Con hardware ESP32 real

1. Abrir `esp32/esp32_sensor.ino` en Arduino IDE
2. Editar las primeras líneas:
   - WIFI_SSID y WIFI_PASSWORD → tu red WiFi
   - DEVICE_NAME → nombre único (sensor-01, sensor-02, etc.)
   - DEVICE_TYPE → tipo de sensor
   - API_URL → IP de tu PC en la red (ver con `ipconfig` en Windows)
3. Subir el firmware al ESP32
4. El sensor aparece automáticamente en el dashboard → Descubrimiento

---

## FIRESTORE REGLAS (pegar en Firebase → Realtime Database → Reglas)

```json
{
  "rules": {
    ".read": true,
    ".write": true
  }
}
```

(Para producción usar reglas más estrictas)

---

## ESTRUCTURA DEL PROYECTO

```
iot-final/
├── backend/
│   ├── server.js              ← API principal
│   ├── init-db.js             ← Cargar datos iniciales
│   ├── simulador.js           ← Simular ESP32 sin hardware
│   ├── serviceAccountKey.json ← Clave Firebase (ya incluida)
│   ├── .env                   ← Variables de entorno (ya configurado)
│   └── package.json
├── frontend/
│   └── index.html             ← Dashboard web
└── esp32/
    └── esp32_sensor.ino       ← Firmware para ESP32
```
