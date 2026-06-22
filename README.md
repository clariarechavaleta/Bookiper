# Bookiper — Sistema Agéntico Contable para PyMEs Uruguay

## Deploy en 3 pasos (gratis, ~15 minutos)

### Paso 1 — Subir a GitHub
1. Crear repo en github.com → "New repository" → nombre: `bookiper`
2. Subir la carpeta `public/` completa

### Paso 2 — Deploy en Vercel (URL pública gratis)
1. Ir a vercel.com → "New Project"
2. Conectar con GitHub → seleccionar repo `bookiper`
3. En "Root Directory" poner: `public`
4. Click "Deploy"
5. En ~2 minutos tenés URL pública: `bookiper-xxx.vercel.app`

### Paso 3 — Configurar Supabase (base de datos gratis)
1. Ir a supabase.com → "New project"
2. Crear tabla `comprobantes` con este SQL:
```sql
create table comprobantes (
  id uuid default gen_random_uuid() primary key,
  proveedor text,
  monto numeric,
  moneda text default 'UYU',
  categoria text,
  estado text,
  latencia numeric,
  usuario text,
  timestamp timestamptz default now()
);
```
3. Ir a Settings → API → copiar "Project URL" y "anon key"
4. En `index.html` reemplazar:
   - `YOUR_SUPABASE_URL` → tu Project URL
   - `YOUR_SUPABASE_ANON_KEY` → tu anon key
5. Hacer commit y push → Vercel redespliega automáticamente

## Arquitectura

```
Usuario (browser)
    ↓
Vercel (frontend HTML)
    ↓
Anthropic API (agentes IA)
    ↓
Supabase (persistencia)
```

## Seguridad
- API key de Anthropic: ingresada por el usuario, guardada en localStorage del browser
- En versión con Cloudflare Worker: la key vive como variable de entorno del Worker
- Google OAuth: autenticación real para acceso a Drive

## Costo mensual estimado
- Vercel: $0 (plan hobby)
- Supabase: $0 (plan free hasta 500MB)
- Anthropic API: ~$3.09/mes para 200 comprobantes
- **Total: ~$3.09/mes**
