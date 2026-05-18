# Deploy — AgriTrace Demo (Vercel)

Demo navegable (CRA). Desplegado en **Vercel** (reemplaza el sandbox
CodeSandbox, que no podía leer el repo privado).

## Primer despliegue (una vez)

1. Ir a <https://vercel.com/new>.
2. **Continue with GitHub** → autorizar Vercel.
3. *Import Git Repository* → si `diegotrujillor/agritrace-demo` no
   aparece (repo privado): **Adjust GitHub App Permissions** → conceder
   acceso a ese repo → volver.
4. Seleccionar `agritrace-demo` → **Import**.
5. Framework: **Create React App** (autodetectado por `vercel.json`).
   No tocar Build/Output (ya definidos en `vercel.json`).
6. **Deploy**. Vercel da una URL `https://agritrace-demo-*.vercel.app`.
7. (Opcional) Project → Settings → Domains → fijar un alias estable
   (ej. `agritrace-demo.vercel.app`).

## Despliegues siguientes

Automático: cada `git push` a `main` → Vercel rebuild + deploy.
Pull requests obtienen Preview Deployments.

## CLI alternativa

```bash
npm i -g vercel
cd agritrace-demo
vercel            # primer run: vincula proyecto (login + scope)
vercel --prod     # despliegue a producción
```

## Verificación post-deploy

`<title>` = `AgriTrace`, `theme-color` = `#2D7A3E`, `/favicon.svg`
servido como `image/svg+xml`, `/manifest.json` con `"name":"AgriTrace
— Trazabilidad agrícola"`.

```bash
curl -sL https://<tu-deploy>.vercel.app | grep -iE '<title>|theme-color'
curl -s -o /dev/null -w '%{content_type}\n' https://<tu-deploy>.vercel.app/favicon.svg
```

## Notas

- `vercel.json`: framework CRA, SPA rewrite a `/index.html`, cache
  inmutable para `/static/*` (assets con hash) y corto para los activos
  de marca.
- Repo privado: Vercel maneja la autorización GitHub de forma nativa
  (a diferencia del sandbox de CodeSandbox).
- Logo/marca: ver `agritrace-docs/03-recursos/brand-guidelines/`.
