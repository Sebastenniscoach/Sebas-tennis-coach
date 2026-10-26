# Sebas Tennis Coach

Aplicación web en español con cinco secciones y panel privado del coach. Frontend React + Vite + Supabase.

## Publicar en Vercel

1. Subir los archivos de esta carpeta **a la raíz** del repositorio GitHub (no subir el ZIP ni la carpeta contenedora).
2. Importar el repositorio en Vercel. Framework: Vite; Build: `npm run build`; Output: `dist`.
3. En Environment Variables configurar:
   - `VITE_SUPABASE_URL` = `https://rbcarhldvmyikipiosuq.supabase.co`
   - `VITE_SUPABASE_ANON_KEY` = clave pública publishable de Supabase (no secret).
4. Deploy. En Supabase > Authentication > URL Configuration, establecer Site URL al dominio HTTPS de Vercel y agregar las Redirect URLs necesarias.
5. Probar inicio de sesión, lectura de servicios y horarios, creación de disponibilidad por el coach y solicitudes de reserva con un alumno de prueba.

## Estado y advertencias

- **No ejecutar** el `schema.sql` del primer prototipo. Esta versión usa las tablas existentes: `services`, `availability`, `bookings`, `coach_admins`.
- Campos asumidos en `services`: `id`, `name`, `duration_minutes`, `price`, `capacity`, `active`. Confirmar `capacity` y `price` antes de publicar; si alguno no existe, quitarlo de la consulta de `services`.
- Campos asumidos en `bookings`: `id`, `player_id`, `availability_id`, `status`, `created_at`. Revisar si existen restricciones adicionales.
- Los posts de noticias, videos, redes y fotos son **contenido de muestra**, no un CMS funcional. El panel permite horarios y gestionar solicitudes solo si las políticas RLS de Supabase lo permiten.
- **IMPORTANTE:** Este MVP aún no evita de forma transaccional reservas simultáneas, no controla cupos de clínicas y no ha sido probado contra el proyecto remoto. Antes de usar con alumnos reales, implementar y probar restricciones/RPC atómicas, estados válidos y políticas RLS. No cobrar ni prometer reservas garantizadas con esta versión.
- La hora mostrada al alumno se presenta en zona America/Mexico_City; los formularios de administración interpretan hora local del navegador del coach.
- No subir `.env` con claves privadas. Solo usar variables de entorno de Vercel. Una clave pública publishable es apta para frontend con RLS correcta.
