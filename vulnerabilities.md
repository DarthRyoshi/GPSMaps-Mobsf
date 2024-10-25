# Vulnerabilidades Identificadas

Este documento presenta las vulnerabilidades detectadas en la aplicación Android tras el análisis de seguridad realizado con MobSF, dividido en análisis estático y dinámico simulado.

---

## Análisis Estático

Estas vulnerabilidades fueron detectadas sin ejecutar la aplicación, únicamente analizando el código y las configuraciones de la APK.

### Vulnerabilidades Críticas (Estático)

1. **Permisos Peligrosos**: La aplicación solicita permisos de ubicación precisa (`android.permission.ACCESS_FINE_LOCATION`) y acceso a la red (`android.permission.INTERNET`) sin implementar medidas de seguridad adicionales, lo que expone a los usuarios a un posible robo de datos de ubicación.

2. **Debugging Activado**: La aplicación tiene el atributo `android:debuggable=true`, permitiendo a atacantes potenciales utilizar herramientas de depuración para inspeccionar y manipular el código de la aplicación, aumentando el riesgo de fuga de información.

3. **Certificado de Depuración**: La aplicación fue firmada con un certificado de depuración, no recomendado para producción, lo que permite a posibles atacantes modificar el código en dispositivos no seguros.

4. **Permiso de Backup Permitido**: La configuración `android:allowBackup=true` permite que usuarios con acceso físico al dispositivo realicen copias de seguridad de los datos de la aplicación, lo cual es un riesgo si contiene información sensible.

---

## Análisis Dinámico (Simulación)

El análisis dinámico simulado se basa en el comportamiento de configuraciones similares en entornos de ejecución y puede incluir vulnerabilidades adicionales no detectables en un análisis estático. A continuación, se destacan las vulnerabilidades simuladas esperadas durante la ejecución de la aplicación.

### Vulnerabilidades Críticas (Dinámico)

1. **Comunicación de Red Insegura**: Aunque la aplicación tiene permisos de red, no se ha verificado el uso exclusivo de HTTPS en el análisis estático. En un entorno dinámico, cualquier conexión HTTP en lugar de HTTPS expone los datos a ataques MITM (Man-in-the-Middle), comprometiendo la seguridad de las comunicaciones.

2. **Exposición Potencial de la Ubicación**: Durante el uso de la aplicación, el permiso de ubicación precisa puede permitir rastrear al usuario en tiempo real, lo que presenta riesgos significativos para la privacidad si se explota por aplicaciones de terceros.

3. **Sesiones Inseguras y Falta de Autenticación Robusta**: No se observó en el análisis estático un sistema de autenticación basado en tokens o expiración de sesión. Esto significa que, en ejecución, una sesión activa podría ser vulnerada, especialmente si no se cierran correctamente las sesiones tras el cierre de la aplicación.

4. **Excesivos Permisos sin Justificación**: En un análisis dinámico, se observaría que la aplicación solicita permisos que no son necesarios para su funcionalidad principal. Esto aumenta la superficie de ataque si aplicaciones de terceros intentan aprovechar permisos innecesarios.

5. **Posible Filtración de Datos en Backup**: El análisis estático ya mostró el permiso de backup habilitado. Durante el uso real, esto permite copiar la información de la aplicación, incluidas configuraciones y datos del usuario, en una copia de seguridad accesible en dispositivos comprometidos.

---

Cada vulnerabilidad detectada en los análisis estático y dinámico resalta áreas críticas para la seguridad y la privacidad de los datos del usuario. Estas deben ser corregidas para cumplir con los estándares de seguridad en aplicaciones Android.
