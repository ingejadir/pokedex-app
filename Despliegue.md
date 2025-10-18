🚀 Proceso de Despliegue — Pokédex Angular en Azure Static Web Apps

Este documento detalla el proceso completo de despliegue de la aplicación Pokédex Angular en Microsoft Azure,
incluyendo la configuración del flujo de CI/CD, los errores presentados, sus soluciones y los resultados finales obtenidos.

1. Configuración Inicial del Proyecto

Requisitos previos:
- Cuenta en Azure for Students o Azure estándar
- Repositorio en GitHub con el código Angular
- Proyecto Angular funcional (verificado con ng serve)

2. Configuración del Recurso en Azure

1. Crear una Static Web App desde el portal de Azure.
2. Conectar el repositorio GitHub y seleccionar el branch main.
3. Configurar los valores:
   - App location: "/"
   - Output location: "dist/pokedex-angular"
4. Azure genera automáticamente un flujo YAML y un token de autenticación.

3. Configuración del Workflow (GitHub Actions)

Archivo: .github/workflows/azure-static-web-apps-ambitious-sky-06d47620f.yml

Este flujo realiza automáticamente:
1. Instalación de dependencias.
2. Compilación del proyecto Angular.
3. Copia de archivos necesarios.
4. Despliegue automático en Azure Static Web Apps.

4. Problemas Detectados Durante el Despliegue
Error	Causa	Solución
No such file or directory: dist/FAEIT.Legacy.IP.Client	Ruta incorrecta en output_location	Corregido a dist/pokedex-angular
Oryx could not detect the language	No se detectó la app Angular	Se ajustó app_location a "/"
Cannot stat staticwebapp.config.json	Archivo mal ubicado	Se movió a la raíz del proyecto
dirname: missing operand	Error en paso de copia	Eliminado paso redundante
npm ERR! ERESOLVE	Conflictos de dependencias	Agregado NPM_CONFIG_LEGACY_PEER_DEPS: true
Process completed with exit code 123	Ruta de index.html incorrecta	Corregido en dist/pokedex-angular
5. Archivo de Configuración staticwebapp.config.json

El archivo define los encabezados de seguridad y reglas de navegación.  
Ubicación: raíz del proyecto Angular.


{
  "globalHeaders": {
    "Strict-Transport-Security": "max-age=31536000; includeSubDomains",
    "X-Frame-Options": "SAMEORIGIN",
    "X-Content-Type-Options": "nosniff",
    "X-XSS-Protection": "1; mode=block",
    "Referrer-Policy": "no-referrer"
  },
  "navigationFallback": { "rewrite": "/index.html" }
}

6. Validaciones del Despliegue

Los flujos #24, #25 y #26 se ejecutaron correctamente:

- #24: Creación de staticwebapp.config.json
- #25: Actualización de rutas e imágenes
- #26: Refactorización final de headers y rutas

7. Resultados Finales

- Despliegue exitoso en Azure ✅
- Certificado HTTPS activo
- Encabezados de seguridad configurados
- Pipeline CI/CD funcionando correctamente
- Calificación A en securityheaders.com

8. Conclusiones y Aprendizajes

- La consistencia entre Angular y el flujo YAML es clave.
- La seguridad web comienza en el proceso de despliegue.
- Automatizar con CI/CD ahorra tiempo y mejora la calidad del producto.


Autor: Inge Jadir  
Colaborador: Arlin Mercado  
Materia: Sistemas Distribuidos  
Fecha: Octubre 2025  
Versión: 1.0

