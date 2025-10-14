# Plantillas del Zettelkasten

Este directorio contiene las plantillas para organizar tu jardín digital como un Zettelkasten.

## Estructura del sistema

```
content/
├── books/          # Una nota por libro leído
├── notes/         # Una cita por archivo (notas fuente)
├── zettelkasten/   # Tu mapa de ideas y conceptos
└── templates/      # Las plantillas (este directorio)
```

## Plantillas disponibles

### 1. `libro-template.md`
Plantilla para crear fichas de libros. Incluye:
- Metadatos del libro (autor, año, ISBN, etc.)
- Espacio para resumen y notas
- Enlaces a citas destacadas
- Sistema de valoración

### 2. `quote-template.md` 
Plantilla para citas individuales. Incluye:
- Referencia al libro origen
- La cita textual
- Tu reflexión personal
- Tags temáticos
- Enlaces relacionados

## Cómo usar las plantillas

### Para crear un nuevo libro:
1. Copia `libro-template.md` a `../books/nombre-del-libro.md`
2. Reemplaza todos los `{{placeholders}}` con la información real
3. El nombre del archivo debe ser en minúsculas y con guiones

### Para crear una nueva cita:
1. Copia `quote-template.md` a `../notes/libro-tema-breve.md`
2. Reemplaza los `{{placeholders}}`
3. Usa tags descriptivos para poder filtrar después

## Ventajas de este sistema

- **Cada cita es independiente** y tiene sus propios tags
- Puedes filtrar por temas usando `/tags/tema`
- Los libros y citas están vinculados bidireccionalmente
- Fácil navegación con los enlaces de Obsidian/Quartz

## Ejemplos

- Libro ejemplo: `../books/sapiens.md`
- Cita ejemplo: `../notes/sapiens-revolucion-cognitiva.md`
