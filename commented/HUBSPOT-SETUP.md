# 📚 GUÍA DE IMPLEMENTACIÓN EN HUBSPOT

## ✅ Archivos Generados

Se han creado dos versiones completamente comentadas de tu página:

| Archivo | Descripción | Uso |
|---------|------------|-----|
| `index-commented.html` | HTML con comentarios detallados | Sube a HubSpot CMS |
| `styles/styles-commented.css` | CSS con documentación completa | Archivo de referencia |
| `index.html` | Versión original optimizada | Producción |
| `styles/styles.css` | Versión original optimizada | Producción |

---

## 🚀 PASOS PARA SUBIR A HUBSPOT

### 1️⃣ PREPARAR CREDENCIALES
Antes de subir, necesitas:
- **Portal ID de HubSpot** (lo encuentras en Configuración)
- **Form ID** del formulario que creaste

**Ubicación en `index-commented.html`:**
```html
<!-- Línea ~80: Reemplaza YOUR_PORTAL_ID -->
<script type="text/javascript" id="hs-script-loader" async defer src="//js.hs-scripts.com/YOUR_PORTAL_ID.js"></script>

<!-- Línea ~850-851: En la función submitHubSpot() -->
const portalId = 'YOUR_PORTAL_ID';  // ← REEMPLAZA AQUÍ
const formId   = 'YOUR_FORM_ID';    // ← REEMPLAZA AQUÍ
```

### 2️⃣ OPCIÓN A: Subir como Página Completa
1. Ve a **Content → Pages** en HubSpot
2. Click en **Create → Website Page**
3. Selecciona **Code view** (esquina superior derecha)
4. Copia TODO el contenido de `index-commented.html`
5. Pega en el editor
6. **IMPORTANTE**: Modifica `YOUR_PORTAL_ID` y `YOUR_FORM_ID` con tus valores reales
7. Copia las rutas de las imágenes al CMS de HubSpot (assets/images/Buho.png)
8. Click en **Publish**

### 3️⃣ OPCIÓN B: Subir como Template Reutilizable
1. Ve a **Design → File Manager**
2. Crea carpeta `/tuttor-up/`
3. Sube:
   - `index-commented.html` (como archivo de referencia)
   - `styles/styles-commented.css` (como Asset)
   - `assets/images/Buho.png` (en Assets)
4. En HubSpot, crea una página y vincula el CSS

### 4️⃣ OPCIÓN C: Usar como Landing Page (Recomendado)
1. Ve a **Tools → Landing Pages**
2. Click en **Create landing page**
3. Selecciona **Blank template**
4. Cambia a **HTML editor** (vista completa)
5. Pega el contenido
6. Modifica credenciales
7. Publica

---

## 🔧 PUNTOS CRÍTICOS A CONFIGURAR

### A. HubSpot Form Integration
```html
<!-- ENCONTRADO EN LÍNEA ~80-81 -->
<script type="text/javascript" id="hs-script-loader" async defer src="//js.hs-scripts.com/YOUR_PORTAL_ID.js"></script>
<script charset="utf-8" type="text/javascript" src="//js.hsforms.net/forms/embed/v2.js"></script>

<!-- ENCONTRADO EN LÍNEA ~798 -->
hbspt.forms.create({
  region: "na1",                    // ← VERIFICA TU REGIÓN (na1, eu1, etc.)
  portalId: "YOUR_PORTAL_ID",       // ← REEMPLAZA
  formId: "YOUR_FORM_ID",           // ← REEMPLAZA
  target: "#hbspt-cta",
  ...
});
```

### B. Campos del Formulario (Línea ~851-870)
Estos campos deben existir en tu HubSpot:
- `firstname` → Nombre
- `lastname` → Apellido
- `email` → Email
- `phone` → Teléfono
- `jobtitle` → Rol (estudiante/tutor)
- `subject__tuttorup` → Materia de interés

**Si tus campos se llaman diferente**, actualiza en la función `submitHubSpot()`:
```javascript
const payload = {
  fields: [
    { name: 'tu_campo_hubspot', value: document.getElementById('f-email').value },
    // ...
  ]
};
```

### C. Assets/Imágenes
La imagen `assets/images/Buho.png` se referencia en:
- Línea 28: Header logo
- Línea 58: Hero section (grande)
- Línea 285: Footer logo
- Línea 600: Logo en CTA

**Opciones:**
1. **Subir a HubSpot File Manager** y actualizar rutas
2. **Usar URL externa** (hosting en otro servidor)
3. **Convertir a Data URI** (embeber en HTML)

**Ejemplo con URL externa:**
```html
<img src="https://tuservidor.com/images/Buho.png" alt="Tuttor-Up">
```

---

## 📋 CHECKLIST ANTES DE PUBLICAR

- [ ] He reemplazado `YOUR_PORTAL_ID` con mi Portal ID real
- [ ] He reemplazado `YOUR_FORM_ID` con mi Form ID real
- [ ] He verificado que mi región es `na1` (o la correcta para mi cuenta)
- [ ] He subido la imagen `Buho.png` a HubSpot y actualizado la ruta
- [ ] He creado los campos del formulario en HubSpot (o renombré los que existen)
- [ ] He testeado el formulario en local antes de publicar
- [ ] He verificado que los links internos (#beneficios, #producto, etc.) funcionan
- [ ] He puesto el sitio en HTTPS (HubSpot lo hace automáticamente)

---

## 🧪 TESTING EN LOCAL (Antes de HubSpot)

```bash
# 1. Abre un servidor local simple
python -m http.server 8000

# 2. Abre en navegador
http://localhost:8000

# 3. Verifica:
#    - Scroll suave funciona ✓
#    - Animaciones corren ✓
#    - Formulario responde a clicks ✓
#    - Responsive en móvil ✓
```

---

## 🎨 PERSONALIZACIÓN VISUAL

### Cambiar Colores
Todos los colores están centralizados en `styles/styles-commented.css` línea 24-29:

```css
:root {
  --teal:       #00d4b8;      /* ← Cambia primario */
  --orange:     #F5A623;      /* ← Cambia secundario */
  --bg-main:    #1a1a2e;      /* ← Cambia fondo */
  /* ... */
}
```

### Cambiar Textos
Busca y reemplaza en `index-commented.html`:
- `Tuttor-Up` → Tu nombre de marca
- `Colombia` → Tu país/región
- URLs en footer (#) → Tus links reales

### Cambiar Animaciones
Encuentra en `styles/styles-commented.css`:
- Línea 1014: `@keyframes owl-float` - velocidad búho
- Línea 1030: `@keyframes ring-expand` - velocidad anillos
- Línea 1050: `@keyframes fc-float` - velocidad tarjetas

---

## 📱 RESPONSIVE BEHAVIOR

| Dispositivo | Cambios |
|------------|---------|
| Desktop (>1024px) | Vista completa con 2-3 columnas |
| Tablet (768-1024px) | 2 columnas → 1-2 columnas |
| Móvil (<768px) | 1 columna, nav contraída, botones apilados |

---

## 🔗 ESTRUCTURA DE SECCIONES

La página está dividida en 10 secciones con IDs para navegación interna:

```html
#hero         → Encabezado principal
#beneficios   → 6 tarjetas de ventajas
#producto     → How it works (4 pasos)
#cta1         → Urgencia (sesión gratis)
#cta2         → Formulario de registro
#testimonios  → Social proof (6 testimonios)
#faq          → Preguntas frecuentes
#prefooter    → Última persuasión
[footer]      → Link footer
```

---

## 💡 FUNCIONES JAVASCRIPT

| Función | Línea | Propósito |
|---------|-------|----------|
| `toggleFaq()` | 817 | Abrir/cerrar FAQ |
| `submitHubSpot()` | 844 | Enviar formulario a HubSpot |
| `hbspt.forms.create()` | 798 | Cargar formulario HubSpot |
| Event listeners | 868+ | Scroll suave y efectos header |

---

## ⚠️ TROUBLESHOOTING

### "El formulario HubSpot no aparece"
✓ Verifica que Portal ID y Form ID son correctos
✓ Revisa que el elemento `#hbspt-cta` existe en HTML
✓ Abre Console (F12) y busca errores de script

### "Las imágenes no cargan en HubSpot"
✓ Sube Buho.png a File Manager de HubSpot
✓ Usa la URL completa que HubSpot te da
✓ O convierte la imagen a Data URI

### "Los links internos no funcionan"
✓ Verifica que existen los IDs (#beneficios, #producto, etc.)
✓ En HubSpot, puede necesitar `/landing-page-url/#beneficios`

### "El CSS no se aplica en HubSpot"
✓ Opción 1: Embeber CSS en `<style>` dentro del HTML
✓ Opción 2: Subir archivo CSS a HubSpot y vincularlo
✓ Opción 3: Usar CSS inline

---

## 📞 SOPORTE Y DOCUMENTACIÓN

- **HubSpot CMS Help**: https://help.hubspot.com/en/articles/3770509-create-a-new-landing-page
- **HubSpot Forms**: https://help.hubspot.com/en/articles/2942215-create-and-publish-a-form
- **Portal ID Location**: Settings > Integrations > APIs & apps

---

## ✨ VERSIONADO

| Versión | Fecha | Cambios |
|---------|-------|---------|
| 1.0 | 2025 | Versión comentada completa |
| Original | 2025 | Versión optimizada para producción |

---

**Última actualización**: Enero 2025
**Autor**: Tuttor-Up Dev Team
**Estado**: Listo para producción ✅
