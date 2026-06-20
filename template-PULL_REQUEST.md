# GUIA PARA ESTRUCTURAR UN BUEN PULL-REQUEST EN GIT

## 1. TÍTULO DEL PR (Claro y descriptivo)
- Usa el formato de Conventional Commits (opcional pero muy recomendado):
  Ejemplo: "feat(autenticación): agregar login con Google OAuth"
  Ejemplo: "fix(api): corregir error 500 en endpoint /users"
  Ejemplo: "docs(readme): actualizar instrucciones de instalación"
- Máximo 50-72 caracteres.
- Resume el cambio en una sola frase que se entienda sin abrir el detalle.

## 2. DESCRIPCIÓN DEL PR (Estructura en tres partes obligatorias)
- ¿QUÉ? -> Explica qué cambio se hizo (el "qué" técnico).
- ¿POR QUÉ? -> Explica la razón del cambio (el problema o necesidad).
- ¿CÓMO? -> Breve resumen de la implementación (solo lo más relevante).

Ejemplo de bloque de descripción:
> "¿Qué? Se agrega la funcionalidad de inicio de sesión con Google OAuth 2.0.
> ¿Por qué? Los usuarios solicitaban un método de acceso más rápido y seguro sin necesidad de registrar contraseña en nuestra plataforma.
> ¿Cómo? Se integró la librería passport-google-oauth20. Se creó el endpoint /auth/google y el callback /auth/google/callback. Se almacena el providerId en la tabla users para futuras asociaciones."

## 3. CONTEXTO Y ENLACES
- Vincula el issue o ticket correspondiente (Jira, GitHub Issue, Trello, etc.) usando palabras clave como "Closes #123" o "Relacionado con PROY-456".
- Si hay discusiones previas o diseños, agrega el enlace directo.

## 4. LISTA DE VERIFICACIÓN PARA EL AUTOR (Checklist)
- [ ] El código compila y pasa todas las pruebas locales.
- [ ] Se agregaron pruebas unitarias / de integración para el nuevo código.
- [ ] La documentación (README, Swagger, comentarios) fue actualizada.
- [ ] No hay código comentado o archivos temporales (logs, .tmp, etc.).
- [ ] Se siguieron las guías de estilo del proyecto (linter / formatter).
- [ ] Los commits están limpios y con mensajes semánticos (no commits tipo "wip" o "fixfix").

## 5. EVIDENCIA Y PASOS PARA PROBAR
- Adjunta capturas de pantalla (UI), logs de consola o salidas de pruebas automatizadas.
- Describe paso a paso cómo probar el cambio manualmente. Ejemplo:
  > "Pasos para probar:
  >  1. Ejecutar npm run dev
  >  2. Ir a http://localhost:3000/login
  >  3. Hacer clic en 'Iniciar con Google'
  >  4. Verificar que se redirige y se crea la sesión correctamente."

## 6. TAMAÑO DEL PR (Regla de oro: PR pequeño y enfocado)
- Un PR debe resolver UNA sola cosa (feature, bugfix, refactor, docs).
- Si excede las 400 líneas modificadas (excluyendo tests o código generado), considera dividirlo en varios PRs.
- Evita mezclar cambios de formato/estilo con cambios funcionales en el mismo PR.

## 7. SOLICITUD DE REVISIÓN (Asignar revisores)
- Asigna al menos 2 revisores si es posible.
- Si hay partes críticas o complejas, menciona directamente a los revisores en el comentario, por ejemplo: "@juan, por favor revisa especialmente la lógica de validación en el middleware".

## 8. NOTAS ADICIONALES (Opcional pero muy útil)
- Indica si hay decisiones técnicas que tomar (trade-offs) o deuda técnica conocida.
- Menciona si hay dependencias externas nuevas que instalar o variables de entorno que agregar.
- Advierte sobre migraciones de base de datos o cambios en el esquema.

## 9. PLANTILLA FINAL (Copia y pega este bloque en tu PR y completa los campos)
```text
Título: <tipo>(<alcance>): <descripción breve>

Descripción:
- Qué:
- Por qué:
- Cómo:

Enlaces:
- Issue: #[número]
- Documentación relacionada: [URL]

Checklist:
- [ ] Código compila y pruebas pasan localmente.
- [ ] Pruebas unitarias agregadas/actualizadas.
- [ ] Documentación actualizada.
- [ ] Código limpio y sin comentarios muertos.
- [ ] Commits semánticos y enfocados.

Cómo probar:
1.
2.
3.

Notas adicionales:
(Decisiones técnicas, dependencias nuevas, o cosas a tener en cuenta)
```

## 10. EXTRAS: BUENAS PRÁCTICAS ADICIONALES PARA EL CONTENIDO
- Sé objetivo y conciso. No escribas párrafos extensos; usa viñetas o frases cortas.
- Si el PR resuelve un bug, describe el bug y cómo se reproduce antes del fix.
- Si es un refactor, explica qué se ganó (rendimiento, legibilidad, mantenibilidad).
- Siempre agradece a los revisores por su tiempo al final del comentario.
- Actualiza el PR si hay comentarios; no resuelvas conversaciones sin aplicar los cambios o sin explicar por qué no se aplican.
