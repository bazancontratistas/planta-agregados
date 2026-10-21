# Control Planta Agregados

App web para el registro diario de ventas, cuadre de mesa, clientes, productos y volquetes.
Funciona en computadora y celular. Los datos se guardan en Firebase (Google) y la página se publica gratis con GitHub Pages.

---

## Lo que necesitas

- Una cuenta de Google (la del dueño).
- Una cuenta de GitHub.
- Unos 15 minutos.

---

## Paso 1. Crear el proyecto en Firebase

1. Entra a <https://console.firebase.google.com> con tu cuenta de Google.
2. **Crear un proyecto** → nombre: `planta-agregados` → puedes desactivar Google Analytics → **Crear proyecto**.

## Paso 2. Activar la base de datos (Firestore)

1. En el menú de la izquierda: **Compilación → Firestore Database → Crear base de datos**.
2. Ubicación: **southamerica-west1 (Santiago)**, la más cercana a Perú. *No se puede cambiar después.*
3. Elige **Iniciar en modo de producción** → **Crear**.

## Paso 3. Registrar la app web y copiar la configuración

1. En **Configuración del proyecto** (el engranaje ⚙ arriba a la izquierda) → **General** → baja hasta **Tus apps** → botón **</>** (Web).
2. Nombre: `planta-web`. **No** marques Firebase Hosting. → **Registrar app**.
3. Te muestra un bloque `const firebaseConfig = { apiKey: "...", ... }`.
4. Abre el archivo **`firebase-config.js`** de esta carpeta y reemplaza cada `PEGA_AQUI...` por el valor correspondiente.

## Paso 4. Activar el inicio de sesión con Google

1. **Compilación → Authentication → Comenzar**.
2. Pestaña **Método de acceso** → **Google** → **Habilitar** → elige tu correo de soporte → **Guardar**.
3. Pestaña **Configuración → Dominios autorizados → Agregar dominio** → escribe `TU_USUARIO.github.io` (tu usuario de GitHub, en minúsculas).

## Paso 5. Poner las reglas de seguridad (muy importante)

1. **Firestore Database → pestaña Reglas**.
2. Borra todo y pega el contenido del archivo **`firestore.rules`**.
3. En la línea `return 'TU_CORREO@gmail.com';` pon **tu** correo de Google (el del dueño).
4. **Publicar**.

Con esto, nadie puede ver ni tocar los datos salvo los correos que tú autorices dentro de la app.

## Paso 6. Subir la app a GitHub

1. En <https://github.com/new> crea un repositorio llamado `planta-agregados`, **público**.
2. **Add file → Upload files** y sube: `index.html`, `firebase-config.js` (ya con tus datos), `firestore.rules` (con `TU_CORREO` sin cambiar) y `README.md`.
   - **No subas** ningún archivo `respaldo-....json`: contiene los datos de tu negocio.
3. **Commit changes**.
4. **Settings → Pages** → en *Branch* elige `main` y `/ (root)` → **Save**.
5. En 1 o 2 minutos tu app estará en: `https://TU_USUARIO.github.io/planta-agregados/`

## Paso 7. Primer ingreso

1. Abre el enlace y toca **Entrar con Google** con el correo del dueño. Entras como **Administrador**.
2. **Ajustes (⚙) → Usuarios**: agrega a Luis y a los trabajadores con su correo de Google y su permiso:
   - **Administrador**: todo, incluidos precios, usuarios y respaldo.
   - **Registra**: tickets, gastos, sencillo, cierres y volquetes.
   - **Solo ve**: consulta y descarga PDF.
3. **Ajustes → Respaldo → Importar respaldo…** y elige `respaldo-inicial.json` para traer los productos, clientes y tickets que ya registraste en la versión de prueba. Si eran solo pruebas, puedes no importarlo y cargar tus productos desde el módulo **Productos**.
4. **Ajustes → Datos de la empresa**: nombre y RUC para los PDF.

En el celular, abre el enlace en Chrome → menú ⋮ → **Agregar a pantalla principal** para tenerla como app.

---

## Uso diario (resumen)

1. **Mañana**: Ventas → Registro del día → *Sencillo del día* (monedas y billetes) → Guardar.
2. **Durante el día**: una fila por ticket. El número de ticket y el monto salen solos.
3. **Cierre**: contar **todo** lo de la mesa (monedas y billetes, incluido el sencillo) → *Cerrar día y descargar PDF* → imprimir y firmar.

## Respaldo semanal

Ajustes → Respaldo → **Descargar respaldo**. Guarda el archivo en tu computadora o Google Drive. El plan gratuito de Firebase no hace copias automáticas.

## Sin internet

Si se va la señal, la app sigue funcionando para gastos, sencillo, cierres y volquetes, y sube los datos cuando vuelve la conexión.
**Los tickets de venta necesitan internet** para sacar el número correlativo sin repetirse.

## Límites del plan gratuito (Spark)

1 GB de datos, 50,000 lecturas y 20,000 escrituras por día. Para una planta con hasta 10 usuarios sobra.

## Cambiar algo de la app

Edita `index.html` (o pídeselo a Claude), súbelo de nuevo a GitHub con **Add file → Upload files** y en un par de minutos se actualiza.
