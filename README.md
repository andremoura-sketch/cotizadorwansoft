# Cotizador Wansoft by Clip

Cotizador interno para el equipo comercial. Wizard paso a paso con catálogo de productos, descuentos y generación de cotización formal vía Claude AI.

## Estructura del proyecto

```
cotizador-wansoft/
├── index.html                  ← cotizador (frontend)
├── netlify.toml                ← configuración de Netlify
├── netlify/functions/
│   └── claude.js               ← proxy seguro a Claude API
└── README.md
```

## Deploy en Netlify (primera vez)

### 1. Sube el repo a GitHub
```bash
git init
git add .
git commit -m "init cotizador wansoft"
git remote add origin https://github.com/tu-org/cotizador-wansoft.git
git push -u origin main
```

### 2. Conecta con Netlify
1. Ve a [netlify.com](https://netlify.com) → **Add new site** → **Import from Git**
2. Selecciona tu repo de GitHub
3. Build settings se auto-detectan desde `netlify.toml`
4. Click en **Deploy site**

### 3. Agrega la API key de Claude
1. En Netlify → tu sitio → **Site configuration** → **Environment variables**
2. Agrega la variable:
   - Key: `CLAUDE_API_KEY`
   - Value: `sk-ant-...` (tu API key de Anthropic)
3. Click **Save** → luego **Deploys** → **Trigger deploy**

### 4. (Opcional) Restringe acceso solo a @clip.com
1. En Cloudflare → **Zero Trust** → **Access** → **Applications**
2. **Add an application** → **Self-hosted**
3. URL: tu dominio de Netlify (ej. `cotizador-wansoft.netlify.app`)
4. Política: `Emails ending in` → `@clip.com`

## Actualizar catálogo o ejecutivos

Edita directamente en `index.html` las constantes `CATALOG` y `EJECUTIVOS` al inicio del `<script>`, luego haz push a GitHub — Netlify redeploya automáticamente en ~30 segundos.

## Actualizar dependencias

El proyecto no tiene dependencias npm. Solo usa:
- [Tabler Icons](https://tabler-icons.io/) via CDN (iconos)
- [Claude API](https://docs.anthropic.com/) via proxy Netlify Function

## Variables de entorno requeridas

| Variable | Descripción |
|---|---|
| `CLAUDE_API_KEY` | API key de Anthropic (sk-ant-...) |
