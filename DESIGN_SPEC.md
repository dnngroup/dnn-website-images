# Especificación de Diseño: dnn_website_images
**ID:** DNN_IMG_DESIGN_V1.1
**Estado:** 📝 DISEÑO PROPUESTO (En Plan Mode)
**Proyecto de Gestión:** `WORK/Projects/Odoo/Global/dnn_website_images`
**Proyecto de Ejecución:** `WORK/Odoo/Global/dnn_website_images`

## 1. Visión General
Suite de snippets de imagen para Odoo 18/19 diseñada para ofrecer una experiencia visual simétrica y funcional, permitiendo tanto la visualización inmersiva (Lightbox) como la navegación dirigida (Grid/Link).

## 2. Componentes (Snippets)

### 2.1 Snippet: Galería Grid/Lightbox (Híbrida)
*   **Comportamiento:** Al hacer click, abre un carrusel Lightbox (Bootstrap 5).
*   **Herencia:** Código optimizado de `ct_website_components`.
*   **Configuración:** Columnas (2, 3, 4, 6), espaciado (Gutter).

### 2.2 Snippet: Galería Grid (Navegacional)
*   **Comportamiento:** Al hacer click, redirige a una URL.
*   **Flujo de Link:** Uso nativo de Odoo (Selección de imagen -> Botón Link del editor).
*   **Simetría y Geometría del Grid:**
    *   **Contenedor (Placeholder):** Cada celda del grid tendrá una relación de aspecto fija (proporción regular largo x ancho). Esto garantiza que todas las filas tengan la misma altura y el grid sea visualmente estable.
    *   **Configuración de Ajuste:** Opción "Ajuste de Imagen" en el panel lateral con valores:
        - **Ajustar (Contain):** Imagen íntegra, sin recortes, centrada en el marco.
        - **Rellenar (Cover):** Imagen llena el marco, recortes automáticos para mantener simetría.
    *   **Estética:** Se podrá configurar un fondo para el contenedor (ej. transparente o color sólido) para rellenar los espacios vacíos en imágenes no proporcionales al marco.
*   **Títulos de Thumbnail:**
    *   **Configuración UI:** Opción "Visibilidad de Título" en el panel de Snippets.
    *   **Valores:** "Siempre Visible" (Always) / "Al pasar cursor" (On Hover).
    *   **Estética:** Overlay inferior semitransparente con texto centrado.
*   **Exhibición:** Sin control de cantidad; muestra el 100% de las imágenes seleccionadas.

## 3. Arquitectura de Implementación
*   **Snippets:** Definidos en `views/snippets/`.
*   **Opciones:** Uso de `website.snippet_options` para inyectar los controles de visibilidad y columnas.
*   **Traducciones:** Soporte multi-idioma nativo para los labels "Always", "On Hover", etc.
*   **CSS:** Uso de `aspect-ratio: 1/1` y `object-fit: cover` para garantizar la simetría independientemente del tamaño original de la imagen.

## 4. Trazabilidad Proyectual
*   **Registro Histórico:** Este diseño nace de la necesidad de estandarizar las galerías de DNN tras el éxito en Carton Trade.
*   **Librarian-Agent:** Auditará que el `README.md` del módulo ejecutable apunte a este documento.

## 5. Estrategia de Compatibilidad Dual (Odoo 18 & 19)
*   **Base Tecnológica:** OWL + Bootstrap 5.
*   **JS Bridge:** Implementación de una capa de detección de versión para invocar el `MediaDialog` correcto según el entorno.
*   **CSS Resiliente:** Uso de selectores agnósticos a la versión del editor para asegurar que el panel de opciones sea funcional en ambos entornos.
*   **Versionamiento:** Se utilizará la base `18.0` como rama principal compatible con 19, a menos que se detecten cambios disruptivos que requieran bifurcación (V.S.B.I).
