# Hotel Bidasoa — Inventory System

Sistema de gestión de inventario en tiempo real para Hotel Bidasoa, desplegado en producción.
Cubre tres puntos de venta con flujos de pedidos, transferencias, ingreso de proveedores y análisis de ventas integrado con el PMS FNSrooms.

## Funcionalidades

**Inventario**
- Stock en tiempo real por ubicación (Bodega · Bar Casa Sanz · Bar Hotel Bidasoa)
- Indicadores visuales de stock mínimo y alertas por email configurables
- Ajuste manual de cantidades con registro de auditoría
- Escáner de código de barras para búsqueda de productos

**Flujo de pedidos**
- Bartenders crean pedidos desde su punto de venta
- Bodeguero aprueba o rechaza con notas, registra la entrega
- Historial completo con trazabilidad por usuario

**Transferencias**
- Movimiento de stock entre ubicaciones con confirmación del receptor

**Ingreso de proveedores**
- Registro de ingresos con número de factura y foto adjunta
- Actualización automática del stock en bodega

**Análisis de ventas**
- Importación de reportes CSV desde FNSrooms (POS)
- Gráficos por familia de producto (cocina / bar / vinos)
- Vista mensual con totales e importes, filtrable por local

**Recetas**
- Catálogo de cócteles y platos con ingredientes y cantidades
- Cálculo de costo por porción
- Importación de recetas desde Casa Sanz

**Panel de administración**
- Gestión de usuarios y roles
- Catálogo de productos y categorías
- Configuración de alertas de stock mínimo

## Roles

| Rol | Acceso |
|---|---|
| `admin` | Acceso completo — usuarios, catálogo, configuración |
| `bodeguero` | Stock, pedidos, transferencias, ingresos |
| `bartender` | Crear pedidos desde su bar, ver stock de su local |

## Stack

**Frontend**
`React 19` `TypeScript` `Vite` `Tailwind CSS` `Radix UI` `Recharts` `React Query`

**Backend & infraestructura**
`Supabase` `PostgreSQL` `Row Level Security` `Edge Functions` `Vercel`

## Estructura del proyecto

```
hotel-inventory/
├── src/
│   ├── components/       # UI por módulo (dashboard, inventory, requests…)
│   ├── pages/            # Vistas principales y panel admin
│   ├── lib/              # Clientes Supabase, parsers CSV, utilidades
│   └── types/            # Tipos TypeScript del dominio
├── supabase/
│   ├── migrations/       # 26 migraciones incrementales
│   └── functions/        # Edge function de notificaciones por email
└── scripts/              # Importación inicial de datos
```

## Variables de entorno

```bash
VITE_SUPABASE_URL=your-supabase-url
VITE_SUPABASE_ANON_KEY=your-supabase-anon-key
```

## Desarrollo local

```bash
npm install
cp .env.example .env   # completar con credenciales de Supabase
npm run dev
```

## Base de datos

Las migraciones están en `supabase/migrations/`. Aplicar en orden con Supabase CLI:

```bash
supabase db push
```
