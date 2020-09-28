---
title: Habilitar el aislamiento de subdominio
intro: 'Puedes configurar el aislamiento de subdominio para separar en forma segura el contenido suministrado por el usuario de las demás partes de tu aparato {{ site.data.variables.product.prodname_ghe_server }}.'
redirect_from:
  - /enterprise/admin/guides/installation/about-subdomain-isolation/
  - /enterprise/admin/installation/enabling-subdomain-isolation
versions:
  enterprise-server: '*'
---

### Acerca del aislamiento de subdominio

El aislamiento de subdominio mitiga las vulnerabilidades del estilo cross-site scripting y otras vulnerabilidades relacionadas. Para obtener más información, consulta "[Cross-site scripting](http://en.wikipedia.org/wiki/Cross-site_scripting)" en Wikipedia. Es altamente recomendable que habilites el aislamiento de subdominio en {{ site.data.variables.product.product_location_enterprise }}.

Cuando el aislamiento de subdominio está habilitado, {{ site.data.variables.product.prodname_ghe_server }} reemplaza varias rutas con subdominios.

| Ruta sin aislamiento de subdominio | Ruta con aislamiento de subdominio |
| ---------------------------------- | ---------------------------------- |
| `http(s)://HOSTNAME/assets/`       | `http(s)://assets.HOSTNAME/`       |
| `http(s)://HOSTNAME/avatars/`      | `http(s)://avatars.HOSTNAME/`      |
| `http(s)://HOSTNAME/codeload/`     | `http(s)://codeload.HOSTNAME/`     |
| `http(s)://HOSTNAME/gist/`         | `http(s)://gist.HOSTNAME/`         |
| `http(s)://HOSTNAME/media/`        | `http(s)://media.HOSTNAME/`        |
| `http(s)://HOSTNAME/pages/`        | `http(s)://pages.HOSTNAME/`        |
| `http(s)://HOSTNAME/raw/`          | `http(s)://raw.HOSTNAME/`          |
| `http(s)://HOSTNAME/render/`       | `http(s)://render.HOSTNAME/`       |
| `http(s)://HOSTNAME/reply/`        | `http(s)://reply.HOSTNAME/`        |
| `http(s)://HOSTNAME/uploads/`      | `http(s)://uploads.HOSTNAME/`      |

### Prerrequisitos

{{ site.data.reusables.enterprise_installation.disable-github-pages-warning }}

Antes de que habilites el aislamiento de subdominio, debes configurar tus ajustes de red para el nuevo dominio.

- Especifica un nombre de dominio válido como tu nombre del host, en lugar de una dirección IP. Para obtener más información, consulta "[Configurar un nombre del host](/enterprise/{{ currentVersion }}/admin/guides/installation/configuring-a-hostname)."

{{ site.data.reusables.enterprise_installation.changing-hostname-not-supported }}

- Configura un registro de Sistema de nombres de dominio (DNS) de carácter comodín o registros DNS individuales para los subdominios detallados más arriba. Recomendamos crear un registro A para `*.HOSTNAME` que apunte a la dirección IP de tu servidor así no tienes que crear múltiples registros para cada subdominio.
- Obtén un certificado de Seguridad de la capa de transporte (TLS) de carácter comodín para `*.HOSTNAME` con un Nombre alternativo del firmante (SAN) para el `HOSTNAME` y para el `*.HOSTNAME` de dominio de carácter comodín. Por ejemplo, si tu nombre del host es `*.github.octoinc.com` obtén un certificado con el valor del nombre común configurado en `*.github.octoinc.com` y un valor SAN configurado en `github.octoinc.com` y `*.github.octoinc.com`.
- Habilita TLS en tu aparato. Para obtener más información, consulta "[Configurar TLS](/enterprise/{{ currentVersion }}/admin/guides/installation/configuring-tls/)."

### Habilitar el aislamiento de subdominio

{{ site.data.reusables.enterprise_site_admin_settings.access-settings }}
{{ site.data.reusables.enterprise_site_admin_settings.management-console }}
{{ site.data.reusables.enterprise_management_console.hostname-menu-item }}
4. Selecciona **Subdomain isolation (recommended)** (Aislamiento de subdominio [recomendado]). ![Casilla de verificación para habilitar el aislamiento de subdominio](/assets/images/enterprise/management-console/subdomain-isolation.png)
{{ site.data.reusables.enterprise_management_console.save-settings }}