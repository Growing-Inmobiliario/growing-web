# PROMPT PARA MARCEL — reconstruir el lead scoring en el servidor
30-oct-2026 · Pásale esto tal cual a su Claude. Es la especificación completa del sistema que estaba corriendo
en el Mac de Pol hasta hoy. El job de Pol ya está apagado, así que no hay riesgo de que se pisen.

---

## CONTEXTO PARA TI, MARCEL (no es parte del prompt)
Lo que tenías montado pinta los eventos de colores en Google Calendar. Lo que Pol quiere recuperar es otra
cosa que iba encima: una **letra de calidad del lead (A, B o C) delante del nombre, junto al color**, calculada
con los datos del formulario y las notas del setter. El título completo queda así:

```
🟡B · Nombre del lead x Growing Inmobiliario
```

El color dice si la cita va a celebrarse. La letra dice si el lead merece preparación. Son dos cosas distintas
y las dos van en el título.

El código que lo hacía está en el Mac de Pol, en `~/growing-ghl/citas_color.py`. Si lo quieres de referencia,
pídeselo. Abajo tienes la especificación completa para no depender de él.

---

# PROMPT (copia desde aquí)

Necesito que montes un proceso que corra cada 15 minutos contra la API de GoHighLevel y mantenga al día el
título, las notas y unos campos de contacto de las citas de auditoría de Growing Inmobiliario.

## 1. QUÉ CITAS

Todas las citas **futuras** (desde ahora hasta 10 días vista) de los calendarios cuyo nombre empieza por
`Auditoría - Growing Inmobiliario (`. Son 27. Hay que leer la lista de calendarios en vivo en cada pasada,
porque se crean calendarios nuevos (el de Hugo-Meta apareció sin avisar).

Se saltan las canceladas y las que el título delate como internas. Filtro de ruido, sobre el título:

```
(1 a 1|entrenamiento|sensei|reuni[oó]n equipo|^equipo |team |llamar |prueba|\btest\b|interna|
onboarding|flight|vuelo|bloque|personal|formaci[oó]n|marcel nadal|coaching|check-in|client succes)
```

**Importante:** NO filtres por «reunión estratégica». Así se titulan las citas que vienen del taller y son
citas de verdad.

## 2. EL TÍTULO

Formato exacto: `{color}{letra} · {nombre} x Growing Inmobiliario`

Ejemplo: `🟡B · Alberto Dominguez x Growing Inmobiliario`

Para construirlo, al título actual se le quita el prefijo anterior si ya lo tiene. Expresión para detectarlo:
`^[🔴🟡🟢][ABC?] · `

## 3. EL COLOR (estado de la cita)

| Color | Cuándo |
|---|---|
| 🔴 | El lead no ha dado señales desde que agendó |
| 🟡 | El lead ha respondido algo después de agendar, o el setter escribió «confirmad…» en una nota |
| 🟢 | 🟡 y además el campo `Confirmado cita` del contacto vale Sí |

Reglas que no se pueden saltar:
- Una cita que ya está en 🟡 o 🟢 **nunca baja a 🔴**. Si la lectura de mensajes falla, se conserva el color
  que ya tenía el título. Un error de red no puede pintar de rojo.
- Para saber si el lead respondió: buscar en sus conversaciones mensajes **entrantes** de tipo
  `TYPE_SMS`, `TYPE_WHATSAPP` o `TYPE_CUSTOM_SMS` posteriores a la fecha de creación de la cita.

## 4. LA LETRA (calidad del lead) — ESTO ES LO IMPORTANTE

Se calcula con una puntuación de 0 a 12. Los pesos salieron de analizar los 1.217 registrados del directo
del 16 de septiembre, mirando qué respuestas separaban a los que agendaban de los que no. **No los cambies
sin hablar con Pol.**

| Dato del lead | Puntos |
|---|---|
| Modo inversión (dice que tiene margen y está listo para invertir) | +3 |
| Tiene inmobiliaria propia | +3 |
| Es agente autónomo | +1 |
| Es agente dentro de una agencia ajena | 0 |
| Factura entre 5.000 y 60.000 €/mes | +2 |
| Factura más de 60.000 €/mes | +1 |
| Más de 1 exclusiva al mes | +1 |
| Usa CRM a diario | +1 |
| Su cuello de botella es «Todo depende de mí» o «Mi equipo no cierra lo que debería» | +1 |

Letra según la puntuación:

| Letra | Puntos |
|---|---|
| A | 8 o más |
| B | de 5 a 7 |
| C | 4 o menos |
| ? | no hay ni tipo de negocio ni facturación |

### 4.1 De dónde salen esos datos: hay TRES formularios distintos

Este es el punto donde es fácil equivocarse. Los leads vienen de tres formularios y cada uno guarda en campos
distintos. Hay que traducir los tres a las mismas preguntas antes de puntuar.

**Formulario del taller** (el más completo). Campos: `Negocio`, `Facturación mes`, `Modo`, `Exclusivas mes`,
`CRM`, `Cuello de botella`.
- `Negocio`: «Tengo mi propia inmobiliaria» → propia · «Soy agente autónomo» → autónomo · «Soy agente en una agencia» → agencia
- `Facturación mes` a tramo: Menos de 5.000 € → 0 · 5.000 – 15.000 € → 1 · 15.000 – 30.000 € → 2 · 30.000 – 60.000 € → 3 · Más de 60.000 € → 4
- `Modo`: si empieza por «Modo inv» → inversión, si no → supervivencia

**Formulario VSL** (lead form de Meta). Campos: `¿Eres el dueño/a de la inmobiliaria? (Lead Form)` y
`¿Cuánto facturaste el último año? (Lead Form)`.
- Dueño: empieza por «Si» → propia · contiene «independiente» → autónomo · resto → agencia
- Facturación anual a tramo mensual: Menos de 100.000 € → 1 · Entre 100.000 y 200.000 € → 1 · Entre 200.000 y 300.000 € → 2 · Entre 300.000 y 500.000 € → 3 · Más de 500.000 € → 4

**Formulario Meta antiguo** (texto libre). Campos: `¿Que tipo de negocio es?` y `¿Estás por encima de €10K/Mes?`.
- Tipo de negocio: si contiene «agente» → autónomo · cualquier otra cosa → propia. Ojo: «Si, lo soy» significa dueño.
- Por encima de 10k: si contiene «no llego» → tramo 0 · cualquier otra respuesta → tramo 1

**Otros dos campos sueltos** que algunos contactos tienen y hay que mirar si los anteriores vienen vacíos:
- `Facturación Mensual`: 1000€-3000€ → 0 · 3000€-6000€ → 0 · 6000€-10.000€ → 1 · 10.000€-20.000€ → 2 · 20.000€-40.000€ → 3 · 40.000€-80.000€ → 3 · 80.000€-120.000€ → 4 · +120.000€ → 4
- `Facturación anual de tu inmobiliaria`: < 100.000€/año → 1 · 100.000 - 250.000€/año → 1 · 250.000€ - 500.000€/año → 2 · 500.000€/año - €1M/año → 3 · €1M/año - €5M/año → 4 · > €5M/año → 4

**Trampa conocida:** el campo `Equipo` guarda por error la respuesta de `Negocio` en 1.060 de 1.184 registros
viejos. Si el valor de `Equipo` es uno de los tres textos de negocio, ignóralo.

**Al leer cualquier campo**, descarta los valores vacíos y los que empiezan por `{{` (merge tags sin resolver).

### 4.2 Las notas del setter mandan sobre el formulario

El setter deja notas en la ficha del contacto, en texto libre, y ahí está la información más fresca y
verificada por teléfono. Lo que diga la nota **pisa** lo que diga el formulario.

Se leen las notas del contacto (`GET /contacts/{id}/notes`), se quita el HTML, se ignoran las que son solo
un id de 20 caracteres, y se procesan con un modelo de lenguaje (nosotros usábamos Claude con salida
estructurada) para extraer: negocio, zona, nº de personas del equipo, facturación mensual en euros,
exclusivas al mes, captaciones al mes, ventas al mes, si puede invertir, problema principal, objetivo y
quién asiste a la reunión.

Con eso se recalcula: si la nota dice la facturación, pisa la del formulario; si dice el tipo de negocio,
pisa el del formulario; si dice que puede invertir y el formulario no traía modo, se cuenta como modo inversión.

**Tres cosas obligatorias en esa extracción:**
1. **Cachear por hash del texto de las notas.** Si las notas no han cambiado, no se vuelve a llamar al modelo.
   Si no, cada 15 minutos estarías pagando por lo mismo. Con caché son céntimos al día.
2. **Solo lo que está en la nota.** Nada inventado. Si no está, campo vacío.
3. **El resumen, el problema y el objetivo los va a leer el cliente** (ver punto 6), así que el modelo tiene
   prohibido valorar su actitud, su dinero o su capacidad de pago. Nada de «muy predispuesta», «escéptico»,
   «desmotivado» ni «liquidez justa». Hechos y cifras, tono de informe.

Si no quieres meter un modelo, el sistema funciona igual solo con los formularios; simplemente habrá más
letras «?» y la ficha será más pobre.

## 5. LOS CAMPOS DE CONTACTO QUE SE ESCRIBEN

Ya existen todos en GHL, creados el 21 de octubre:

| Campo | Qué se escribe | Id |
|---|---|---|
| `Lead · Banda` | A, B, C o ? | xMCi7wY6clBhez1pQJJ3 |
| `Lead · Puntos` | la puntuación, o vacío | Q6l05gwX6bbynw1e82Dz |
| `Cita · Color` | rojo, amarillo o verde | pMkqoHqgmyCYI8mefMpP |
| `Cita · Calculado el` | fecha y hora de la pasada | PLlMI1GMvCUxQpZNs7WW |
| `Cita · Ficha setter` | el resumen de las notas | 5gnBTOkAbzG3uKeKNApm |

## 6. LA FICHA EN GOOGLE CALENDAR

GoHighLevel **ignora el campo `notes` cuando actualizas una cita**: puedes mandarlo, devuelve 200 y no hace
nada. La única forma de que la información aparezca en la descripción del evento de Google es la **plantilla
`notes` del calendario**, con merge tags. Ya está puesta en los 27 calendarios y es esta:

```
Factura: {{contact.facturacin_mes}} · Negocio: {{contact.negocio}} · {{contact.exclusivas_mes}} exclusivas/mes
Zona: {{contact.en_qu_zona_trabaja}}
Momento de inversión: {{contact.modo}}
Cuello: {{contact.cuello_de_botella}}
Setter: {{contact.setter_responsable}} · Vídeo visto: {{contact.vdeo_tarea_visto}} · Confirmada: {{contact.confirmado_cita}}
Anuncio: {{contact.utm_content}}
Campaña: {{contact.utm_campaign}} · Conjunto: {{contact.utm_term}}
Setter dice: {{contact.cita__ficha_setter}}
- - - - - - - - - -
```

Google solo la vuelve a renderizar **cuando se actualiza la cita**. Como el proceso actualiza el título cada
vez que cambia algo, se renderiza sola.

**Orden obligatorio al escribir:** primero los campos del contacto, luego la cita. Si lo haces al revés,
Google renderiza la plantilla con los valores viejos.

**Y una advertencia:** el lead está invitado al evento, así que **ve el título y la descripción**. Por eso en
la plantilla no hay ni color en palabra ni banda ni puntos: eso va solo en el título y en los campos internos.
Si añades algo a la plantilla, piensa que lo va a leer el cliente.

## 7. TRAMPAS DE LA API DE GOHIGHLEVEL (nos costaron tiempo)

- **`PUT /calendars/{id}` NO es parcial.** Si mandas solo un campo, los que omitas se resetean: `openHours`
  se vacía, `slotDuration` y `slotInterval` vuelven a 30, `formSubmitType` pasa a ThankYouMessage. Hay que
  leer la config entera, quitar las claves de solo lectura (`id`, `locationId`, `dateAdded`, `dateUpdated`,
  `traceId`, `calendarType`, `groupId`, `isActive`, `slug`, `widgetSlug`), renombrar `formSubmitRedirectUrl`
  a `formSubmitRedirectURL`, y mandarlo todo. Después, releer y comprobar que el único campo que ha cambiado
  es el que querías. A nosotros esto nos dejó un calendario sin huecos reservables durante 15 minutos.
- **`PUT /calendars/events/appointments/{id}`**: manda siempre `toNotify: false` y
  `ignoreFreeSlotValidation: true`. Sin el primero, el lead recibe un correo de actualización cada vez.
- `GET /calendars/events` quiere `startTime` y `endTime` en **milisegundos epoch**. Con fechas ISO devuelve
  lista vacía sin dar error.
- Los mensajes de una conversación vienen anidados en `messages.messages`.
- Version header: `2021-07-28`. Host: `services.leadconnectorhq.com`.

## 8. SEGURIDAD, QUE ESTO ES PRODUCCIÓN

1. **Snapshot antes de la primera escritura**: guardar la config completa de los 27 calendarios y el título
   y las notas de todas las citas futuras. Y un modo de restaurar desde ese snapshot.
2. **Modo simulación por defecto.** Que escriba solo con un `--execute` explícito.
3. **Log de todo lo que se escribe**, con fecha, qué cita, qué había antes y qué hay después.
4. **Solo escribe lo que cambia.** Comparar título y campos antes de mandar nada.
5. **Reintentos ante caídas de red**, y si una lectura falla, conservar el valor anterior en vez de calcular
   uno nuevo con datos incompletos.

## 9. CÓMO SABER QUE ESTÁ BIEN
- Una cita cuyo lead factura 20.000 €/mes, tiene inmobiliaria propia y está en modo inversión tiene que salir
  con 8 puntos o más, o sea banda A.
- Un lead sin ningún formulario sale con `?`.
- El título de una cita ya marcada en 🟡 no puede volver a 🔴 en la siguiente pasada.
- Al actualizar una cita, en Google Calendar aparece la ficha con la facturación y el «Setter dice» rellenos.
- Ningún lead recibe un correo de Google diciendo que su cita se ha actualizado.
