SIGNAM · Firebase integrado / auto conexión

Base utilizada:
- SIGNAM_FIREBASE_DB_MAQUETA.html

Archivo final:
- SIGNAM_FIREBASE_AUTO_CONFIG.html

Objetivo:
- Evitar que el usuario tenga que pegar firebaseConfig cada vez.
- Dejar el proyecto Firebase signam-produccion incrustado dentro del HTML.
- Conectar automáticamente a Firebase al abrir la app.
- Mantener modo avanzado para cambiar de proyecto si fuera necesario.

Firebase integrado:
- projectId: signam-produccion
- authDomain: signam-produccion.firebaseapp.com
- storageBucket: signam-produccion.firebasestorage.app
- messagingSenderId: 806512509339
- appId: 1:806512509339:web:b5984c4e884f7ce4b6613e

Cambios realizados:
1. Se agregó SIGNAM_FIREBASE_DEFAULT_CONFIG dentro del código.
2. La app intenta conectar automáticamente con signamDbConnect(true) al cargar.
3. La sección Base de Datos ya no exige pegar configuración.
4. Se agregó modo “Configuración avanzada” para reemplazar localmente el config si se requiere.
5. Se conservó botón Conectar / Reconectar.
6. Se actualizó el estado de conexión para indicar si usa configuración integrada o avanzada.
7. Se mejoró el parser para aceptar tanto JSON como bloque JS tipo const firebaseConfig = {...};

No se tocó:
- CSV Admira.
- Layout obligatorio ARTICULOS,BRANDS,CENTROS,CIRCUITO,RESOLUCION,RETAILERS.
- Control de Testigos.
- Subpestañas Resumen / Operativo.
- Navegación principal.
- Lógica Proveedor vs Institucional.
- Sincronización incremental ya existente.

Validación técnica:
- Se extrajeron scripts del HTML.
- Se validó sintaxis con node --check sin errores.

Notas de seguridad:
- firebaseConfig no es una clave privada.
- La protección real debe estar en Firebase Authentication y Firestore Security Rules.
- Las reglas mínimas recomendadas son request.auth != null para las colecciones SIGNAM.
- Para producción real se recomienda endurecer reglas por correo, dominio o roles.

Uso esperado:
1. Abrir HTML desde servidor local, por ejemplo:
   python -m http.server 8000
2. Abrir:
   http://localhost:8000/SIGNAM_FIREBASE_AUTO_CONFIG.html
3. Ir a Base de Datos.
4. Ver estado de conexión.
5. Cargar archivo operativo.
6. Ejecutar Sincronizar líneas operativas.

Si la conexión falla:
- Confirmar que Authentication Anonymous esté habilitado.
- Confirmar que Firestore esté creado.
- Confirmar que Rules permitan read/write con request.auth != null.
- Confirmar conexión a internet porque el SDK Firebase se carga desde CDN.
