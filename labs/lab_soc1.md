#  Laboratorio SOC Analyst L1 – Análisis de Fuerza Bruta en Windows

##  Objetivo
Practicar el rol de un **SOC Analyst Nivel 1** detectando un ataque de fuerza bruta en logs de Windows.  

---

##  Dataset
Usaremos eventos de ejemplo del repositorio público [EVTX-ATTACK-SAMPLES](https://github.com/sbousseaden/EVTX-ATTACK-SAMPLES).  

Descarga el archivo:  
 [Brute Force – Windows Security Log (evtx)](https://github.com/sbousseaden/EVTX-ATTACK-SAMPLES/blob/master/Account%20Discovery/Brute%20Force/Security.evtx)  

---

##  Pasos del análisis

1. **Abrir los logs**
   - En un equipo Windows, abre **Event Viewer** (`eventvwr.msc`) o una herramienta como [Event Log Explorer](https://eventlogxp.com/) o [Chainsaw](https://github.com/WithSecureLabs/chainsaw).  
   - Carga el archivo `Security.evtx`.  

2. **Eventos relevantes a revisar**
   - **4625 (Failed Logon)** → Intento fallido de inicio de sesión.  
   - **4624 (Successful Logon)** → Inicio de sesión exitoso.  
   - **4672 (Special Privileges Assigned)** → Indica uso de cuentas con privilegios.  

3. **Detectar el patrón sospechoso**
   - Busca **múltiples 4625 seguidos de un 4624 exitoso** desde la misma IP o con el mismo usuario.  
   - Esto indica un posible **ataque de fuerza bruta exitoso**.  

4. **Extraer IoCs (Indicadores de Compromiso)**
   - Nombre de usuario atacado.  
   - Dirección IP de origen.  
   - Horario del ataque.  
   - Hostname de destino.  

---

##  Ejemplo de hallazgos

- **Usuario atacado:** `Administrator`  
- **IP atacante:** `192.168.1.50`  
- **Eventos detectados:** 30 intentos fallidos (4625) seguidos de 1 éxito (4624).  
- **Riesgo:** Acceso no autorizado con privilegios.  

---

##  Actividad del estudiante

1. Revisa los logs y encuentra el patrón descrito.  
2. Documenta el incidente como si fueras SOC L1.  

Ejemplo de reporte rápido:
