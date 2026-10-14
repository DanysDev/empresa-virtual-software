# Requerimientos · <slug> <vN>

## 1. Metadata
- id: AR-AAAAMMDD-XX · fecha: AAAA-MM-DD
- fuente: [brief.md, cambios.md, investigacion.md]
- autor_analisis: "analista-requerimientos"
- estado: borrador | pendiente-confirmacion | confirmado

## 2. Contexto resumido
(solo hechos fieles a las fuentes)

## 3. Conflictos resueltos
- id · entre [brief/cambios] · descripción · resolución · evidencia · impacto

## 4. Ambigüedades detectadas
- id · expresión · origen · acción (pasado_a_du | requiere_confirmacion)

## 5. Objetivo de la versión
(medible, sí/no) + criterios de verificación (1-2 observables)

## 6. Alcance MVP
- id · descripción · por qué es imprescindible · origen

## 7. Fuera de alcance
- id · descripción · motivo · origen (pospuesto vs descartado, sin solape con §6)

## 8. Requisitos Funcionales (RF-XX)
- RF-01: El sistema DEBE… (EARS si aplica · prioridad Must/Should/Could · origen · criterio de prueba · INVEST ok)

## 9. Requisitos No Funcionales (RNF-XX)
- RNF-01: … (categoría · umbral + unidad · método de verificación · origen)

## 10. Casos de Uso (CU-XX)
- **CU-01: Nombre (verbo + objeto)**
  - Actor: … · Objetivo: … · Pre: … · Post: …
  - Flujo principal: 1. … 2. …
  - Alternativos: … · Excepciones: … · Reglas: RB-XX
  - Relacionados: RF-XX · Origen: …

## 11. Entidades (conceptuales)
- **ENT-XX Nombre:** descripción · atributos mínimos (tipo lógico, obligatorio, razón de uso) · id lógico · relaciones MVP · usado por RF/CU

## 12. Reglas de Negocio (RB-XX)
- **RB-01 Nombre:** enunciado determinista · tipo · origen · aplicable a · cómo verificarse · relacionados RF/CU/ENT

## 13. Dudas por confirmar (DU-XX)
- **DU-01:** pregunta directa · contexto · afecta a · prioridad Alta/Media/Baja · bloquea MVP [sí/no] · texto para el responsable · evidencia origen

## 14. Gaps detectados
- id · tipo (rf_sin_cu | cu_sin_rf | rb_sin_cobertura | ent_sin_uso | solape) · acción (eliminar | pasar_a_du | corregir) · resuelto [sí/no]

## 15. Trazabilidad resumida
(tabla RF ↔ CU ↔ RB ↔ ENT)

## 16. Checklist validación final
fuentes [ok/no] · medibles [ok/no] · sin solape [ok/no] · sin invención [ok/no] · dudas cubren huecos [ok/no] · trazable [ok/no] · coherente [ok/no] · sin técnico [ok/no] · sin diseño [ok/no] · objetivo verificable [ok/no]
