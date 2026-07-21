# El Taray compartido: puesta en marcha

Esta versión funciona de dos maneras:

- **Modo local:** abre el HTML y guarda los datos en ese navegador.
- **Modo nube:** publicada en GitHub Pages y conectada a Firebase, todos ven y modifican los mismos datos en tiempo real.

Antes de empezar, abre **Datos → Copia de seguridad (.json)** y guarda una copia.

## 1. Crear el proyecto de Firebase

1. Entra en Firebase Console y crea un proyecto nuevo, por ejemplo `el-taray-reservas`.
2. En la página principal del proyecto, pulsa el icono **Web `</>`**.
3. Registra una app web. No hace falta activar Firebase Hosting.
4. Firebase mostrará un bloque parecido a:

```js
const firebaseConfig = {
  apiKey: "...",
  authDomain: "...",
  projectId: "...",
  storageBucket: "...",
  messagingSenderId: "...",
  appId: "..."
};
```

Guarda ese bloque. Se pegará después dentro de la aplicación.

## 2. Activar el acceso con contraseña compartida

1. En Firebase abre **Authentication**.
2. En **Método de acceso**, activa **Correo electrónico/contraseña**.
3. En **Usuarios**, crea un único usuario compartido.
4. Usa un correo válido y una contraseña que solo conozca la familia.

La contraseña no se pega en el HTML ni queda guardada en su código. Cada navegador la usa para iniciar sesión en Firebase.

## 3. Crear Firestore

1. En Firebase abre **Firestore Database**.
2. Pulsa **Crear base de datos**.
3. Elige el modo de producción y una región europea próxima.
4. Abre la pestaña **Reglas**.

Las reglas exactas se generan dentro de la app:

1. Abre **Datos**.
2. Escribe el correo compartido y el nombre del espacio, por ejemplo `el-taray`.
3. En el bloque **Reglas de seguridad de Firestore**, pulsa **Copiar reglas**.
4. Pégalas en Firebase y pulsa **Publicar**.

No uses reglas que permitan leer o escribir a cualquiera.

## 4. Publicar el HTML en GitHub Pages

1. Crea un repositorio nuevo en GitHub, por ejemplo `el-taray-reservas`.
2. Sube el archivo `index.html` a la raíz del repositorio.
3. En el repositorio abre **Settings → Pages**.
4. En **Build and deployment**, selecciona **Deploy from a branch**.
5. Elige la rama `main`, carpeta `/ (root)`, y guarda.
6. GitHub mostrará una dirección parecida a:

```text
https://TU-USUARIO.github.io/el-taray-reservas/
```

Ese es el enlace que se comparte con la familia.

> Con una cuenta gratuita de GitHub, normalmente el repositorio de Pages será público. El HTML y la configuración pública de Firebase podrán verse, pero la contraseña no está dentro del archivo y Firestore debe quedar protegido por Authentication y sus reglas.

## 5. Conectar la aplicación

Desde el navegador que contiene la versión correcta de los datos:

1. Abre la dirección de GitHub Pages.
2. Pulsa **Datos**.
3. En **Configuración Firebase**, pega el bloque `firebaseConfig` completo.
4. Escribe el correo compartido.
5. Deja `el-taray` como espacio compartido, salvo que quieras otro nombre.
6. Pulsa **Guardar configuración**. La página se recargará.
7. Vuelve a **Datos**, escribe la contraseña y pulsa **Conectar y sincronizar**.

Si el espacio de Firestore está vacío, este primer navegador subirá automáticamente sus datos locales. Por eso debe hacerse primero desde la copia que consideres correcta.

## 6. Acceso de las demás personas

Cada persona:

1. Abre el mismo enlace de GitHub Pages.
2. En **Datos**, pega la misma configuración de Firebase una sola vez.
3. Usa el mismo correo, espacio y contraseña.
4. Pulsa **Conectar y sincronizar**.

A partir de ahí, los cambios en reservas distintas se sincronizan entre dispositivos. Si dos personas modifican exactamente la misma reserva casi al mismo tiempo, prevalece la última escritura recibida.

## 7. Qué se sincroniza

- Reservas, una por documento independiente.
- Habitaciones, reglas fijas, ramas y preferencias.
- Base de personas y compatibilidades.
- Plegatín, avisos y texto pendiente.

Los cambios de interfaz que todavía no se hayan aplicado, como una propuesta de distribución abierta, no se sincronizan hasta pulsar **Aplicar**.

## 8. Copias de seguridad

Aunque uses Firebase, descarga periódicamente una copia desde:

**Datos → Copia de seguridad (.json)**

Para recuperarla:

**Datos → Restaurar copia (.json)**

Al restaurar una copia mientras estás conectado, los datos restaurados se enviarán a la nube.

## 9. Botón Datos en móvil

En móvil, **Datos** abre una hoja desde la parte inferior de la pantalla. Se cierra con la `×`, tocando fuera del panel o pulsando Atrás/Escape cuando el navegador lo permita.
