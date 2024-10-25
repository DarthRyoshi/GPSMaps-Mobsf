# Vulnerabilidades Identificadas

Este documento presenta las vulnerabilidades detectadas en la aplicación Android tras el análisis de seguridad realizado con MobSF.

## Vulnerabilidades Críticas
1. **Permisos Peligrosos**: Se detectó que la aplicación solicita permisos de ubicación precisa y acceso a la red sin implementar seguridad adicional, lo cual representa un riesgo de exposición de datos sensibles.
2. **Debugging Activado**: La aplicación tiene el atributo `android:debuggable=true`, lo cual permite que atacantes potenciales utilicen herramientas de depuración para inspeccionar el código, aumentando el riesgo de fuga de información.
3. **Certificado de Depuración**: La aplicación fue firmada con un certificado de depuración, que no es adecuado para producción y permite a posibles atacantes manipular el código en dispositivos no seguros.
4. **Permiso de Backup Permitido**: La aplicación tiene el permiso `android:allowBackup=true`, lo cual permite a usuarios que tengan acceso físico al dispositivo realizar copias de seguridad de los datos de la aplicación.

Cada vulnerabilidad documentada aquí afecta directamente a la seguridad y privacidad de los datos del usuario, por lo cual su corrección es esencial.
