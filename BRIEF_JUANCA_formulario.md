# BRIEF PARA JUANCA — Formulario «Confirma tu auditoría»
v1 · 23-oct-2026 · De: Pol · Para: Juanca (embudo + GHL)

La web ya está hecha y publicada. Lo que falta es conectarla a GoHighLevel y montar los dos workflows.
Tiempo estimado: 1-2 horas.

---

## 1. QUÉ ES Y POR QUÉ

Formulario que el lead rellena **después de agendar la auditoría y antes de la reunión**. No cualifica
(eso ya lo hizo el formulario de registro): su único trabajo es que el lead **se comprometa por escrito**
y nos dé munición para preparar la reunión.

Está diseñado sobre tres cosas de Cialdini: el compromiso vale más si es escrito, activo y voluntario;
la gente cumple lo que ha dicho con sus propias palabras; y el plan «si pasa X, entonces hago Y» funciona
porque la decisión se toma antes de que llegue la excusa.

**Dos números para entender la urgencia:**
- Show-up actual 42-55 %. El objetivo de la brújula (32 presentadas con 46 citas) necesita 70 %.
- De 46 reuniones descualificadas en octubre, 7 lo fueron solo porque faltaba un socio en la llamada.
  La cláusula tercera de este formulario existe para eso.

### Dónde encaja en el flujo
```
Anuncio → Página A (VSL + agenda) → CITA AGENDADA
   → WhatsApp: vídeo 60 s de Pol + «contéstame con un 👍»
   → 👍 del lead
   → WhatsApp: enlace a ESTE FORMULARIO
   → el lead lo rellena (2 min)
   → PÁGINA DE GRACIAS: manual «Las etapas de crecimiento de una inmobiliaria» + vídeo de Juanca
   → mañana de la cita: llamada del closer
   → T-60 min: enlace de Zoom
   → REUNIÓN
```

---

## 2. LA WEB (ya está hecha, no hay que diseñar nada)

- **Publicada en:** https://growing-inmobiliario.github.io/growing-web/confirma_auditoria.html
- **Repositorio:** github.com/Growing-Inmobiliario/growing-web (público)
- **Archivos:** `confirma_auditoria.html` (todo el formulario, CSS y JS dentro) + `logo_growing.png`
- **Prueba con datos:** añade `?nombre=Gloria&apellidos=Mulet&dia=22/10/2026%2011:00` al final de la URL

### Diseño: sistema «Escritura»
Es el lenguaje visual nuevo de Growing: **todo lo que publicamos parece un papel de notaría**.
A partir de aquí, web, landings y documentos van en este estilo. El manual completo está en
`MANUAL_MARCA_ESCRITURA.md` y la hoja de estilos reutilizable en `escritura.css`.

- **Una sola tipografía:** Courier Prime (Google Fonts, gratis), como una máquina de escribir.
- **Títulos pequeños** en mayúsculas con mucho espaciado, nunca titulares grandes.
- **Fondo blanco**, hoja blanca con grano de papel casi imperceptible. Nada oscuro.
- **Paleta Templanza:** Tinta #10141F · Latón #C0A46B (sello) · Lacre #B5382A (botón) · Petróleo #135E6E (foco).
- **Membrete** con el logo arriba a la izquierda, FOJAS a la derecha, sello circular girado.
- **Cifras en letra y número:** «tres (3) meses», «veinticuatro (24) horas».
- **Cláusulas numeradas** PRIMERO.- SEGUNDO.- … Una por pantalla, estilo Typeform.
- **Botón-sello rojo lacre** al final: «CONFIRMO MI AUDITORÍA».

### Comportamiento
- Una cláusula por pantalla con Siguiente / Atrás.
- Enter avanza. En los campos de texto largo, ⌘/Ctrl + Enter.
- En las preguntas de una sola opción, al marcar pasa sola a la siguiente.
- No deja avanzar sin contestar; el aviso sale en rojo debajo.
- Progreso en la línea de registro: «CLÁUSULA TERCERA · 3 DE 6».
- Al enviar: sello CONFIRMADA + «Hecho, [nombre]» y redirección a la página de gracias.

---

## 3. LAS SEIS CLÁUSULAS (texto literal, no cambiar)

### PRIMERO.- Del problema
**Pregunta:** Si en esta hora resolviéramos un solo problema y ese problema multiplicara tu negocio, ¿cuál sientes que es?
**Contexto:** Marca el que de verdad te frena.
**Opciones (una):**
- No consigo noticias de propietarios que quieran vender y dependo principalmente de referidos
- Tengo citas de captación, pero mi equipo o yo no cerramos las propiedades necesarias en exclusiva y en precio
- Necesito nuevas personas en mi equipo para lograr los objetivos y no tengo buenos procesos de contratación
- No sé dónde está ahora mismo mi principal problema
- Otro → abre un campo de texto

**Segundo campo, opcional:** «Si quieres, añade lo que hoy frena el crecimiento de tu inmobiliaria.
Cuanto más sepamos, mejor preparamos tu caso. *(opcional)*»

### SEGUNDO.- De los números
**Pregunta:** Tus dos números de los últimos tres (3) meses.
**Contexto:** Una aproximación vale. Estos datos no se usan para nada más: sirven para orientar la reunión e ir directos a tu problema.
**Campos:** Captaciones (unidades) · Facturación (€)

### TERCERO.- De quién comparece a la reunión
**Pregunta:** ¿Quién decide en tu inmobiliaria?
**Contexto:** Los mejores resultados los conseguimos cuando todos los socios están alineados desde el primer día.
Si un socio no puede estar en la reunión, buscaremos otra fecha en la que estéis todos, para asegurar el éxito de cada cliente.
**Opciones (una):** Yo · Mi socio/a y yo, y venimos los dos a la reunión

### CUARTO.- De los imprevistos
**Pregunta:** Si el [día] a las [hora] te surge una visita, una firma o un cliente, ¿qué harás?
**Opciones (una):** Mantengo la reunión y muevo lo otro · Os aviso con veinticuatro (24) horas de antelación y la cambiamos, una sola vez

### QUINTO.- De la disposición
**Pregunta:** El [día] a las [hora] estaré…
**Contexto:** Marca las dos. Una auditoría desde el coche con el móvil no sirve de nada.
**Casillas (las dos obligatorias):** En un ordenador con cámara · En un sitio tranquilo

### SEXTO.- De la firma
**Campo:** Nombre y apellidos
**Casilla obligatoria:** «Yo, [nombre], entiendo que esta cita es importante para mí y confirmo mi asistencia.
También entiendo que si no aparezco sin avisar o cancelo a última hora sin motivo, no podré volver a acceder
a una auditoría personalizada de mi negocio con Growing Inmobiliario.»

**Botón:** CONFIRMO MI AUDITORÍA
**Pie:** Este documento no tiene valor legal. Tiene valor de palabra.

---

## 4. LO QUE HAY QUE HACER EN GHL

### 4.1 Crear 9 campos de contacto
| Campo | Tipo |
|---|---|
| Reunión · Problema | TEXT |
| Reunión · Frenos | LARGE_TEXT |
| Reunión · Captaciones trimestre | NUMERICAL |
| Reunión · Facturación trimestre | NUMERICAL |
| Reunión · Decisor | TEXT |
| Reunión · Si surge algo | TEXT |
| Reunión · Preparado | TEXT |
| Reunión · Firma | TEXT |
| Reunión · Formulario | TEXT |

### 4.2 Crear un Inbound Webhook
Workflow nuevo → trigger **Inbound Webhook** → copiar la URL.
La página le manda un POST con JSON. Payload exacto:

```json
{
  "cid": "ID del contacto en GHL",
  "email": "", "tel": "", "nombre_url": "", "dia": "jueves 22 de octubre", "hora": "11:00",
  "problema": "texto de la opción marcada (o 'Otro: …')",
  "frenos": "texto libre, puede venir vacío",
  "captaciones_trimestre": 12,
  "facturacion_trimestre": 45000,
  "decisor": "Yo | Mi socio/a y yo, y venimos los dos a la reunión",
  "si_surge": "Mantengo la reunión y muevo lo otro | Aviso con 24 horas…",
  "preparado": "Sí",
  "firma": "Nombre y apellidos",
  "compromiso": "Sí",
  "formulario": "Sí",
  "enviado": "2026-10-23T10:15:00.000Z"
}
```

El workflow busca el contacto por `cid` (o por email si falta) y rellena los 9 campos.
Añade el tag `confirmado-formulario`.

### 4.3 Poner las dos URLs en el HTML
Al principio del `<script>` hay un bloque CONFIG con dos líneas vacías. Rellenar y avisar a Pol
(Claude lo vuelve a subir a GitHub en 20 segundos):

```js
const CONFIG = { WEBHOOK_URL: "https://…", GRACIAS_URL: "https://…" };
```

### 4.4 El enlace que manda GHL por WhatsApp
Tiene que llevar estos parámetros, con merge tags:

```
https://growing-inmobiliario.github.io/growing-web/confirma_auditoria.html?nombre={{contact.first_name}}&apellidos={{contact.last_name}}&cid={{contact.id}}&email={{contact.email}}&tel={{contact.phone}}&dia={{appointment.start_time}}
```

El campo `dia` admite formato ISO o `22/10/2026 11:00`; la página lo convierte sola
a «jueves 22 de octubre» y «11:00».

### 4.5 Página de gracias (pendiente de construir)
Mismo estilo escritura. Lleva, en este orden:
1. «Hecho, [Nombre]. Tu hora está reservada y tu caso en preparación.»
2. **Regalo:** botón de descarga del manual «Las etapas de crecimiento de una inmobiliaria» (PDF)
   + el mismo PDF por WhatsApp automático.
3. Vídeo de Juanca: qué pasa desde que un cliente paga hasta que tiene resultados.
4. Testimonios.

### 4.6 Los mensajes
**Tras el 👍 (automático):**
> «Perfecto, [Nombre]. Antes de vernos, 2 minutos: [enlace]. Con lo que escribas preparamos tu caso,
> y al terminar te llevas "Las etapas de crecimiento de una inmobiliaria" para ver en cuál estás.»

**Si a las 24 h no lo ha rellenado (lo manda el setter a mano, uno solo):**
> «[Nombre], me faltan tus 2 minutos para preparar tu caso del [día]: [enlace].»

**Si el día antes sigue sin formulario:** el setter llama. La cita sigue en 🔴 y su hueco admite un segundo lead.

---

## 5. CÓMO LO USA EL EQUIPO

- **El color de la cita** (🔴🟡🟢 en el título de Google Calendar) lo calcula un script cada 15 minutos.
  Decisión pendiente de Pol: si el 🟡 lo da el 👍 o el formulario enviado.
- **Las respuestas aparecen solas en la ficha de Google** de la cita, en la línea «Setter dice»,
  porque los 27 calendarios de auditoría ya llevan la plantilla con merge tags.
- **El closer** entra a la reunión con el problema marcado, los dos números y quién decide.

---

## 6. LO QUE NO LLEVA, A PROPÓSITO

- Precio, oferta ni condiciones. Eso es de la reunión.
- Preguntas de cualificación largas: ya están en el formulario de registro.
- Más de una pregunta abierta obligatoria: la gente abandona a la tercera.
- Nada de «escalar»: decimos **hacer crecer tu inmobiliaria**.

---

## 7. MEDICIÓN (a las 4 semanas)

Show-up de tres grupos: sin 👍 · con 👍 pero sin formulario · con formulario enviado.
Si el formulario no separa, se cambia. Lo saca Claude del CRM.

---

## 8. QUIÉN HACE QUÉ

| Tarea | Quién |
|---|---|
| Los 9 campos de contacto | Juanca |
| Inbound webhook + workflow que rellena los campos | Juanca |
| Página de gracias (estilo escritura) | Claude monta el HTML, Juanca la conecta |
| PDF «Las etapas de crecimiento de una inmobiliaria» | Pol (decide si existe o se redacta) |
| Vídeo de Juanca (qué pasa cuando pagas) | Juanca |
| Vídeo de 60 s de bienvenida | Pol |
| Workflows de WhatsApp (👍, formulario, T-60) | Juanca |
| Subir cambios de la web a GitHub | Claude |
