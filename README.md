# AgroConnect – Frontend (Next.js + TypeScript + Tailwind)

Plataforma que conecta agricultores con compradores. Paleta verde, App Router.

## Correr en local

```bash
npm install
npm run dev        # http://localhost:3000
```

## Subir a Vercel

1. Sube esta carpeta a un repositorio de GitHub.
2. En vercel.com → **Add New → Project** → importa el repo (Vercel detecta Next.js solo).
3. **Deploy**. (Las variables de Supabase se agregan en el siguiente paso.)

## Rutas (pantallas)

| Ruta | Pantalla |
|---|---|
| `/` (`app/page.tsx`) | Inicio + formulario para elegir **Agricultor / Comprador** |
| `/agricultor/registro` | Crear cuenta (Continuar con Google o correo) |
| `/agricultor/datos` | Nombres, apellidos, nacimiento, correo, usuario, contraseña, foto |
| `/agricultor/finca` | Perfil de la chacra / finca |
| `/agricultor/publicaciones` | Publicaciones anteriores + ventana **Ofrecer lote de cosecha** (pestañas *Datos del lote* y *Detalles extra*) |
| `/agricultor/pago` | QR de Yape y cálculo automático del 7% |
| `/comprador` | ¿Persona o empresa? |
| `/comprador/persona/registro` | Crear cuenta (Google o correo) |
| `/comprador/persona/datos` | Datos + preferencias de compra + foto → **Crear perfil** |
| `/comprador/empresa` | Nombre comercial, RUC, preferencias → **Guardar e ingresar** |
| `/lotes` | **Lotes en venta** (búsqueda y filtros) |
| `/lotes/[id]` | Producto, detalles, perfil del productor, historial de ventas, **Estoy interesado / Volver** (WhatsApp, llamada, correo) |

## Formularios

Cada formulario tiene un `handleSubmit` que hoy hace `console.log` con los datos
**ya en el formato de las tablas** de `supabase/schema.sql` (nombres en snake_case).
Busca el comentario `// SUPABASE (siguiente paso):` en cada archivo: ahí va la llamada real.

```
components/forms/
  AgricultorDatosForm.tsx   → usuarios
  FincaForm.tsx             → fincas, finca_certificaciones
  OfrecerLoteModal.tsx      → lotes, lote_fotos
  PagoYapeForm.tsx          → pagos_publicacion
  PersonaDatosForm.tsx      → usuarios, perfiles_comprador, preferencias_compra
  EmpresaForm.tsx           → empresas, preferencias_compra
components/AccionesLote.tsx → contactos
```

## Siguiente paso: conectar Supabase

1. `npm install @supabase/supabase-js`
2. Copia `.env.local.example` → `.env.local` y llena `NEXT_PUBLIC_SUPABASE_URL` y `NEXT_PUBLIC_SUPABASE_ANON_KEY`
   (y agrégalas también en Vercel → Settings → Environment Variables).
3. Descomenta `lib/supabase.ts`.
4. Ejecuta `supabase/schema.sql` en Supabase → SQL Editor.
5. Reemplaza los bloques `SUPABASE (siguiente paso)` y los datos de ejemplo de `lib/data.ts`.

## Qué personalizar

- `lib/constants.ts` → `YAPE`: titular, número y QR real (pon la imagen en `/public` y su ruta en `qrSrc`).
- `lib/constants.ts` → `COMISION_PORCENTAJE` (7 por defecto).
- `lib/data.ts` → datos de ejemplo (números de WhatsApp en formato `51XXXXXXXXX`).
- Colores en `app/globals.css` (`--color-hoja`, `--color-bosque`, etc.).
