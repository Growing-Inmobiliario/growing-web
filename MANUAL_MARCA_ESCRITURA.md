# MANUAL DE MARCA «ESCRITURA» — Growing Inmobiliario
v1 · 22-oct-2026 · Para web, landings, formularios, PDFs y documentos. Fuente de verdad: `escritura.css`.

## 1. La idea en una frase
No hacemos pantallas. Hacemos papeles. Todo lo que publica Growing parece una escritura, una nota simple o un expediente de notaría:
papel, máquina de escribir, texto justificado, cláusulas numeradas, un sello y un timbre. Es el sector inmobiliario sin decirlo.

Lo que transmite: seriedad, cosa firmada, consecuencias. Un dueño de inmobiliaria firma escrituras: lo reconoce al instante.

## 2. La tipografía, sacada de la escritura
La escritura real (notaría, Iquique, 2011) está escrita a máquina: una sola familia monoespaciada, un solo tamaño, y la jerarquía
se hace con MAYÚSCULAS, negrita y espaciado, nunca con tamaños grandes.

- Familia única: **Courier Prime** (Google Fonts, gratis; es la Courier bien dibujada). Respaldo: Courier New.
  Enlace: `https://fonts.googleapis.com/css2?family=Courier+Prime:ital,wght@0,400;0,700;1,400&display=swap`
- Cuerpo: 16 px en escritorio, 15 px en móvil. Interlineado 1,75. **Justificado**, como en el papel.
- Títulos: el MISMO tamaño que el cuerpo (máximo 1,05 rem), en mayúsculas, negrita y espaciado de letras 0,22 em.
  Nada de titulares de 60 px. En una escritura el título es pequeño y centrado.
- Nombres propios (personas, empresas): **MAYÚSCULAS NEGRITA** dentro del párrafo, como «LUISA PATRICIA CRUZATT OVALLE».
- Cifras importantes: se escriben en letras y luego en número, como en la escritura: «tres exclusivas (3) al mes».
- Separadores: una línea de asteriscos `******` o un filete en latón. Nunca iconos.
- Numeración: PRIMERO.-  SEGUNDO.-  TERCERO.- … Cada sección de una landing es una cláusula.
- Al pie: número de página centrado. Arriba a la derecha: «FOJAS» con un número.
- El único adorno tipográfico permitido es la cursiva de Fraunces para el tagline «Recupera tu vida.» junto al logo. Nada más.

## 3. Paleta Templanza (solo estas)
| Nombre    | Hex      | Uso                                                        |
|-----------|----------|------------------------------------------------------------|
| Tinta     | #10141F  | La mesa (fondo de la página fuera del papel) y texto fuerte |
| Papel     | #F4F1E8  | El papel                                                    |
| Piedra    | #EFEDE6  | Papel alternativo, fondos claros                            |
| Latón     | #C0A46B  | Sello, filetes, detalles. Nunca texto largo                 |
| Lacre     | #B5382A  | Timbre, botón-sello, errores. UNA cosa en lacre por página  |
| Petróleo  | #135E6E  | Enlaces, foco de campos                                     |
| Gris      | #6B675E  | Notas al margen, «para qué»                                 |
El cian #2CB9D9 es solo del logo. Las fotos van en blanco y negro (como en un expediente).

## 4. Anatomía de un documento (en este orden)
1. **Sello** en latón, arriba a la derecha, girado -12°. Texto en círculo: GROWING INMOBILIARIO · lo que sea el documento.
2. **Cabecera**: marca a la izquierda (GROWING INMOBILIARIO + línea pequeña gris), FOJAS a la derecha.
3. **Línea de asteriscos** · REG. … Nº · FECHA · **línea de asteriscos**.
4. **Título** en mayúsculas espaciadas: CONFIRMACIÓN DE AUDITORÍA / AUDITORÍA PERSONALIZADA / PROPUESTA…
5. **Las partes**: «NOMBRE DEL LEAD · a · GROWING INMOBILIARIO».
6. **Timbre** en lacre (opcional): lo que se entrega o la promesa. Girado -1°.
7. **Comparecencia**: un párrafo en prosa de escritura: «Comparece DON …, titular de su inmobiliaria, y declara …».
8. **Cláusulas** PRIMERO.- … con una línea gris de «para qué» debajo del título.
9. **Firma** y **botón-sello** en lacre (la única llamada a la acción).
10. Nota al pie en gris y número de página.

## 5. Componentes (clases de escritura.css)
- `.mesa` + `.papel`: la hoja sobre la mesa. `.papel--piedra` para variante.
- `.cab`, `.asteriscos`, `.reg`: cabecera notarial.
- `h1`, `.partes`, `.timbre`, `.sello`, `.filete`.
- `.clausula` + `h2` (con `<span>` para el subtítulo gris) + `.porque`.
- Formularios: `.campo` (línea de máquina), `textarea.campo` (renglones), `.opcion` + `.caja` (casillas X y radios ●), `.dos` (dos columnas), `.error`.
- `.sellar` (botón-sello lacre), `.sellar--laton` (secundario), `.pie`, `.nota-pie`.
- `table.cuentas` (libro de cuentas, números tabulares), `.video` (vídeo como foto pegada), `.numpag`.

## 6. Cómo se convierte una landing en un documento
- Hero = portada de la escritura: sello, cabecera, título pequeño, las partes, un párrafo de comparecencia. Sin imagen de fondo.
- Cada sección = una cláusula numerada. El texto se lee de arriba abajo como un contrato, no se escanea.
- Beneficios = «DECLARACIONES»: lista con guion largo, no iconos ni tarjetas.
- Precio o números = `table.cuentas`.
- Testimonios = «TESTIGOS»: nombre en MAYÚSCULAS NEGRITA, ciudad, una frase entre comillas.
- VSL o vídeos = `.video`, como una foto pegada al expediente, con pie en mayúsculas pequeñas.
- CTA = un solo botón-sello en lacre por página. Texto en primera persona: «CONFIRMO MI AUDITORÍA», «QUIERO MI AUDITORÍA».
- Formularios = cláusulas con campos de línea. Las casillas se marcan con X.

## 7. Lo que no se hace
- Degradados, tarjetas con esquinas redondeadas, sombras de colores, iconos, emojis en la página.
- Más de una tipografía. Más de un color de acento por página.
- Titulares gigantes. Fotos a color. Animaciones de entrada.
- Texto centrado en párrafos largos (solo títulos y partes van centrados).
- «Escalar» como palabra de marca: decimos **hacer crecer tu inmobiliaria**.

## 8. Accesibilidad y móvil
- Contraste texto/papel ≥ 10:1. Lacre sobre papel ≥ 5:1 solo para texto corto y en mayúsculas.
- Mínimo 15 px en móvil. Campos y casillas de 20 px, zona táctil ≥ 44 px (el `.opcion` entero es clicable).
- Foco visible en petróleo. Funciona sin JavaScript para leer; con JS para enviar.

## 9. Archivos
- `escritura.css`: tokens y componentes. Se enlaza en toda página nueva.
- `confirma_auditoria.html`: primer documento hecho con el sistema (formulario de confirmación). Sirve de plantilla.
- Pendiente de crear con el mismo sistema: página de gracias (manual + vídeo de Juanca), Página A (VSL + agenda), landing de la web.
