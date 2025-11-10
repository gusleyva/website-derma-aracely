# Landing de la Dra. Aracely Castillo (Dermatóloga)

Proyecto de landing page profesional, estática y con foco en SEO, construida con Astro + Tailwind CSS.

## Objetivos
- Presentación clara de servicios y credenciales (CILAD) con diseño elegante.
- SEO técnico sólido (meta, Open Graph, accesibilidad básica, performance).
- Despliegue en servidor propio con archivos estáticos (sin runtime en producción).

## Stack
- Astro (SSG • 100% estático, excelente SEO y performance)
- Tailwind CSS (utilidad + variables CSS para paleta)

## Paleta de colores
- `--primary`: `#b88a8f`
- `--secondary`: `#dcb7b9`
- `--text`: `#4e3a3c`

Definidas en `src/styles/global.css` y aplicadas en `Layout.astro`.

## Estructura inicial
- `src/layouts/Layout.astro`: Layout base con `<head>` SEO por defecto y Tailwind importado.
- `src/styles/global.css`: Tailwind + variables de color.
- `astro.config.mjs`: Tailwind integrado vía `@tailwindcss/vite`.

## SEO inicial
En `src/layouts/Layout.astro` se incluyen:
- `<title>` y `<meta name="description">` descriptivos.
- `<meta name="keywords">`.
- Open Graph básico (`og:title`, `og:description`, `og:type`, `og:locale`).
- `theme-color` usando el color primario.

Siguientes mejoras (próximas iteraciones):
- Etiquetas OG con imagen social (`og:image`) y `twitter:card`.
- Schema.org (JSON-LD) para médico/centro clínico.
- Sitemap y robots.txt (Astro soporta fácilmente archivos estáticos).

## Desarrollo
- Iniciar dev server:
  - `npm run dev`
- Compilar build estático:
  - `npm run build`
- Previsualizar build:
  - `npm run preview`

## Despliegue en servidor propio (Nginx)
1) Construir: `npm run build` → genera `dist/`.
2) Copiar `dist/` al servidor (ej.: `/var/www/derma`).
3) Configuración Nginx (ejemplo mínimo):

```
server {
    listen 80;
    server_name ejemplo.derma.mx;  # Cambiar por el dominio real

    root /var/www/derma;
    index index.html;

    location / {
        try_files $uri $uri/ /index.html;
    }

    # Estáticos con cache
    location ~* \.(?:css|js|jpg|jpeg|png|gif|svg|ico|webp)$ {
        expires 30d;
        add_header Cache-Control "public, max-age=2592000, immutable";
    }
}
```

4) HTTPS: instalar Certbot y emitir certificado Let’s Encrypt.

## Próximos pasos sugeridos
- Crear páginas/secciones: `index.astro` con hero, sobre, servicios, testimonios, contacto.
- Componente `Seo.astro` para sobrescribir título/descripcion por página cuando se requiera.
- Optimizar imágenes (Astro `<Image />` / imágenes locales) y favicon.
- Añadir `sitemap.xml` y `robots.txt`.

---

Si deseas, puedo continuar creando la estructura de secciones con el diseño propuesto y contenido de ejemplo en español.
