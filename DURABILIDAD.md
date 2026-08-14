# Continuidad de Raices

Este sitio usa Supabase como fuente viva del arbol. En el plan gratis, Supabase puede pausar proyectos con poca actividad durante una semana. Para una version familiar de largo plazo, hay tres capas recomendadas:

1. **Disponibilidad real:** mover el proyecto de Supabase a Pro. Es la unica forma simple de evitar pausas automaticas por inactividad.
2. **Keepalive:** usar `.github/workflows/supabase-keepalive.yml` para hacer una lectura diaria/periodica del snapshot y generar actividad.
3. **Preservacion:** exportar periodicamente una copia privada del snapshot y de los archivos del bucket `family-media`.

## Configuracion del keepalive

En GitHub, agregar estos valores al repositorio:

- Secret `SUPABASE_URL`: `https://czjjzfovdnrsqowecuol.supabase.co`
- Secret `SUPABASE_ANON_KEY`: la clave publica anon/publishable usada por el frontend.

El workflow llama la funcion publica `raices_keepalive()` tres veces al dia. Esa funcion solo devuelve estado y hora del servidor; no entrega personas, relaciones, historias ni archivos, y no necesita la clave familiar.

El repositorio tambien incluye `.github/workflows/repository-keepalive.yml`, que hace un commit tecnico mensual en `.github/keepalive-stamp.txt`. Esto mantiene actividad en GitHub para reducir el riesgo de que se desactiven los workflows programados del repositorio publico.

## Limites importantes

- El keepalive reduce el riesgo de pausa, pero no es una garantia contractual.
- En repositorios publicos, GitHub puede desactivar workflows programados si no hay actividad en el repositorio durante 60 dias.
- Para que el arbol siga disponible por generaciones, la decision mas robusta es Supabase Pro mas respaldos privados periodicos.
