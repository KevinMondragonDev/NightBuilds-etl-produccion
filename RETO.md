# 🚀 Reto 3 — Un ETL a producción

**Repositorio:** `NightBuilds-etl-produccion` · **Nivel:** avanzado · **Entorno:** Floci (S3, Step Functions, Lambda, SQS, Secrets Manager) + PostgreSQL · **Método y evaluación:** [`README.md`](docs/METODO.md)

## El caso

Tienes un pipeline que funciona cuando tú lo ejecutas. Tu jefa te dice: «El lunes lo dejamos corriendo solo. Si falla a las tres de la mañana, quiero enterarme antes que el cliente, y que lo pueda arreglar quien esté de guardia aunque no seas tú». Eso es llevarlo a producción.

No construyes un pipeline nuevo: partes de uno tuyo (por ejemplo `NightBuilds-pipeline-banco`) y lo vuelves **operable**.

## Lo que debe existir al terminar

- **Infraestructura como código:** un comando crea todos los recursos desde cero y otro los destruye. Nada creado a mano.
- **Orquestación** con reintentos, esperas y un camino claro cuando algo falla (Step Functions o Airflow).
- **Despliegue automático:** cada cambio pasa por pruebas y análisis de estilo antes de llegar a la rama principal.
- **Observabilidad:** logs estructurados, tres métricas que importen (por ejemplo filas procesadas, duración y antigüedad del último dato) y una alerta que se dispare de verdad.
- **Calidad de datos como freno:** si los datos no pasan las comprobaciones, no se publican.
- **Seguridad:** ningún secreto en el código ni en Git; permisos mínimos escritos para cada pieza; datos personales enmascarados.
- **Guía de operación** (*runbook*): qué hacer ante los tres fallos más probables, escrita para alguien que no conoce el proyecto.
- **Un tablero de salud en D3.js**, servido por una API: estado de las últimas ejecuciones, duración y volumen.

## Restricciones

- Otra persona ejecuta tu guía de operación ante un fallo provocado, **sin preguntarte nada**. Si no puede, no está terminado.
- Relanzar cualquier día deja el mismo resultado.
- El emulador no aplica los permisos de IAM: escríbelos igualmente y explica cada acción permitida.

## Preguntas que tu diseño debe responder

- ¿Cómo te enteras de que el pipeline **no se ejecutó**? (No es lo mismo que «falló».)
- ¿Qué pasa si se ejecuta dos veces a la vez?
- ¿Cuánto tarda en notarse un dato malo y hasta dónde llega antes de que lo notes?
- ¿Qué es lo que más cuesta de tu diseño en AWS real y cómo lo abaratarías?

## Defensa: lo que te van a preguntar

- Provocamos un fallo en vivo: tumba la base, sube un archivo roto o corta la red. Enséñanos qué pasa.
- ¿Qué pieza dejaste sin vigilar y por qué puedes vivir con ello?
- Vuelve a la versión anterior del pipeline. ¿Cuánto tardas?

## Súbelo de nivel

- Despliégalo en la capa gratuita de AWS con una alerta de facturación, y destrúyelo al terminar.
- Añade un entorno de pruebas separado del de «producción», con la misma infraestructura como código.
- Mide cuánto cuesta cada ejecución y redúcelo a la mitad.
