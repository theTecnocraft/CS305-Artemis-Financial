# CS 305 — Portafolio de Artemis Financial

**Autor:** Francis Joseph Anton Giler  
**Artefacto seleccionado:** Informe de prácticas para un software seguro, Proyecto final II.

Este repositorio reúne el informe completo y una reflexión sobre el desarrollo de un prototipo local para Artemis Financial. El proyecto demuestra el cálculo de una huella SHA-256 y la comunicación mediante HTTPS.

- [Informe completo del Proyecto final II](Anton_Francis_CS305_Proyecto_Final_II.docx)
- [Proyecto Maven, código, pruebas y evidencias](CS305_Proyecto_Final_II_Artemis.zip)

El ZIP contiene su propio README con las instrucciones de ejecución y los informes originales. Los resultados descritos a continuación corresponden a las ejecuciones documentadas en el proyecto; no representan un análisis actualizado ni una garantía de ausencia de vulnerabilidades.

## 1. Cliente y requisitos del software

Mi cliente en este proyecto académico fue Artemis Financial. La necesidad abordada consistía en comprobar la integridad de los datos y proteger su comunicación. Para ello desarrollé un prototipo que calcula una huella SHA-256 y presenta el resultado mediante HTTPS. El alcance fue una demostración local: no procesa operaciones financieras, no almacena cuentas y no incorpora autenticación de clientes ni transferencia de archivos.

## 2. Decisiones acertadas e importancia del código seguro

Una decisión acertada fue combinar la revisión del código con el análisis de dependencias y las pruebas funcionales. El primer análisis de la versión modernizada señaló once identificadores CVE asociados a Tomcat 11.0.24. Revisé los avisos del proveedor, actualicé Tomcat a 11.0.27 y repetí la verificación, sin añadir supresiones ni elevar los umbrales para ocultar resultados. También diferencié la detección de un componente vulnerable de la demostración de una explotación real.

Desarrollar código seguro ayuda a proteger los datos y a reducir fallos, interrupciones y costes de corrección. Para una empresa, la seguridad contribuye a la continuidad del servicio y a la confianza de sus clientes. En este trabajo fue especialmente importante distinguir la integridad que aporta el hash de la protección del canal que proporciona TLS.

## 3. Parte más útil de la evaluación

Una de las partes más útiles del proceso fue interpretar los resultados y sus límites. El informe de dependencias incluía 41 objetos principales y 27 registros relacionados: 68 entradas examinadas, no 68 bibliotecas distintas. También fue necesario distinguir el uso de HTTPS de la confianza en la identidad del servidor. El navegador mostraba una advertencia por el certificado autofirmado, mientras que el cliente de pruebas validaba el certificado al confiar explícitamente en el CER. Estas comprobaciones muestran por qué un resultado debe analizarse junto con su contexto y sus evidencias.

## 4. Refuerzo de las capas de seguridad y recursos futuros

Reforcé varias capas: utilicé SHA-256 de la biblioteca estándar de Java, configuré HTTPS con TLS 1.2 y 1.3, mantuve la contraseña del almacén fuera del código y limité el servidor al equipo local. Añadí cabeceras restrictivas, desactivé la carga multipart, limité las peticiones y evité exponer mensajes y trazas internos. Además, reduje dependencias innecesarias y separé las responsabilidades del servicio de hash, el controlador y el filtro de cabeceras.

En futuros trabajos emplearía análisis de dependencias con datos actualizados, avisos oficiales de los proveedores, documentación de OWASP y revisión manual del código. Seleccionaría las mitigaciones según los componentes afectados, su exposición y el impacto en la aplicación. Para una ampliación a producción también evaluaría autenticación, autorización, gestión y renovación de secretos, certificados del dominio real y pruebas del despliegue.

## 5. Verificación de funcionalidad y seguridad tras la refactorización

Comprobé el comportamiento mediante la compilación, ocho pruebas JUnit y catorce comprobaciones externas satisfactorias. Comparé el hash con un cálculo independiente en Python y probé valores conocidos, entrada vacía, rechazo de null, alteración de datos y concurrencia. Las pruebas externas comprobaron HTTPS, cabeceras, respuestas de error y rechazo de certificados sin confianza o nombres de servidor incorrectos.

Después de refactorizar y actualizar las dependencias, repetí las pruebas y Dependency-Check y revisé las clases modificadas. El análisis final registró cero vulnerabilidades en la instantánea utilizada, cuya última comprobación de datos NVD fue el 12 de octubre de 2026. La actualización en línea había fallado, por lo que ese resultado no cubre avisos posteriores ni demuestra que no exista ninguna vulnerabilidad. La combinación de revisión y pruebas aportó evidencia para detectar regresiones dentro del alcance del laboratorio.

## 6. Recursos, herramientas y prácticas reutilizables

Utilicé Java, Spring Boot, Maven, JUnit, OWASP Dependency-Check, Eclipse, keytool y un cliente de pruebas en Python. Me serán útiles la separación de responsabilidades, la inyección por constructor, el uso de estado inmutable y una instancia independiente de MessageDigest por cálculo. También reutilizaría la gestión de contraseñas mediante variables de entorno, la validación de certificados sin desactivarla y la conservación de registros e informes que permitan reproducir y revisar los resultados.

## 7. Evidencia para futuros empleadores

Podría presentar el informe completo, el código refactorizado, las pruebas automatizadas, el certificado público y los informes de dependencias antes y después de la actualización. Estas evidencias muestran mi capacidad para interpretar hallazgos, aplicar mitigaciones, verificar el comportamiento y documentar decisiones técnicas. También permiten explicar los límites del trabajo con precisión: el prototipo es local, emplea un certificado autofirmado y requiere controles adicionales y un análisis actualizado antes de considerarse apto para producción.
