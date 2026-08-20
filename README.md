# Nuestro Dinero

Aplicación móvil-first para que Piero y Mafer registren gastos, ingresos, presupuestos y estadísticas compartidas. Está creada con una identidad visual original en azul noche y celeste, sin assets de franquicias.

## Tecnologías

- Vite + JavaScript ES modules
- Firebase Firestore (SDK modular)
- HTML/CSS responsivo, PWA básica y GitHub Pages

## Ejecutar

```bash
npm install
npm run dev
npm run build
```

## Firebase

La configuración está en `src/firebase/firebase-config.js`. El proyecto entregado ya incorpora la configuración proporcionada. En Firebase Console, crea una base Firestore y comienza en modo de prueba únicamente durante desarrollo.

Colecciones usadas: `movimientos`, `categorias`, `presupuestos` y, preparada para evolución, `configuracion`, `gastosRecurrentes`, `metasAhorro`.

Los movimientos se consultan por `mes` y luego se ordenan por `fecha`; si Firestore solicita un índice compuesto, crea el índice para `movimientos(mes ASC, fecha DESC)`.

### Reglas de desarrollo

```text
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /{document=**} { allow read, write: if true; }
  }
}
```

Estas reglas permiten que cualquiera con acceso al proyecto lea y escriba. Al no haber autenticación, Firestore no puede limitar de forma real el uso solamente a Piero y Mafer. Ocultar la configuración de Firebase tampoco protege Firestore. Antes de uso real, evalúen Firebase Authentication o un backend seguro.

## GitHub Pages

El workflow `.github/workflows/deploy.yml` publica cada push a `main`. En GitHub, habilita **Settings → Pages → Source: GitHub Actions**. Vite aplica automáticamente la subruta `/nuestro-dinero/` durante el build de Actions.

## Estructura

`src/firebase` contiene integración; `services` CRUD; `pages` las vistas; `components` interfaz reutilizable; `state` cache en memoria; `utils` fechas, moneda y cálculos; `constants` el dominio.
