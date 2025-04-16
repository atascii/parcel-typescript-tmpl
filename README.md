## 🛠️ Opción 1: Compilar solo con `tsc` (TypeScript Compiler)

Si lo único que querés es compilar los `.ts` a `.js` sin bundling ni optimización (es decir, un build más crudo), podés usar `tsc` directamente.

### 1. Asegurate de tener un `tsconfig.json`, algo como esto:

```json
{
  "compilerOptions": {
    "outDir": "dist",
    "target": "es6",
    "module": "es6",
    "moduleResolution": "node",
    "strict": true,
    "esModuleInterop": true,
    "sourceMap": true
  },
  "include": ["src/**/*.ts"]
}
```

### 2. Agregá este script:

```json
"tscbuild": "tsc"
```

Este comando compilará todo el TypeScript desde `src/` hacia `dist/` respetando la configuración de tu `tsconfig.json`.

---

## 📦 Opción 2: Usar Parcel pero sin HTML (solo TS)

Si querés usar Parcel **con su sistema de bundling**, pero sin el HTML como punto de entrada, podés hacer algo como esto:

```json
"parcel-tsbuild": "parcel build src/main.ts"
```

Parcel tomará `main.ts` como entrada y generará un bundle con todos los módulos importados. Esto puede ser útil si tu proyecto es una librería o backend, o si tenés múltiples archivos `.ts` y querés un **único archivo compilado**.

### Resultado típico
- Entrada: `src/main.ts`
- Salida (en `dist/`): `main.[hash].js`

💡 Asegurate de no tener referencias al DOM si no hay HTML involucrado.

---

## 📦 Opción 3: Compilar varios archivos TS como entradas

Si tenés múltiples archivos de entrada (por ejemplo `main.ts`, `admin.ts`, `dashboard.ts`), podés hacerlo así:

```json
"parcel-tsbuild": "parcel build src/main.ts src/admin.ts src/dashboard.ts"
```

Parcel va a generar un bundle separado por cada uno.

---

### Nota:
Si querés conservar estructura original y módulos separados, la mejor forma es usar el compilador de TypeScript (tsc) directamente.

Como se indicó anteriormente:

```json
"tscbuild": "tsc"
```

---
## Guia de scripts

- Parcel para desarrollo y build final (parcel-build, dev)
- Parcel solo con TS como entrada (parcel-tsbuild) (compila en un solo archivo .js)
- Compilación TypeScript sin bundling (tscbuild) (compila con tsc, genera varios archivos si es necesario)
- Servidor estático para la dist (serve)
- Script para limpiar clean