---
author: PatAltimore
ms.service: active-directory-b2c
ms.topic: include
origin.date: 11/03/2016
ms.date: 04/04/2019
ms.author: v-junlch
ms.openlocfilehash: 4d5c8373f2a8f02ccfbe51cb970ab08744950e7e
ms.sourcegitcommit: 61c8de2e95011c094af18fdf679d5efe5069197b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62128220"
---
[!INCLUDE [active-directory-b2c-portal-add-application](active-directory-b2c-portal-add-application.md)]

Para registrar la aplicación web, use la configuración que se especifica en la tabla.

![Ejemplo de configuración de registro para la nueva aplicación web](./media/active-directory-b2c-register-web-app/b2c-new-app-settings.png)

| Configuración      | Valor de ejemplo  | DESCRIPCIÓN                                        |
| ------------ | ------- | -------------------------------------------------- |
| **Nombre** | Aplicación B2C de Contoso | Escriba un **Nombre** para la aplicación que la describa a los consumidores. | 
| **Incluir aplicación web o API web** | Sí | Seleccione **Sí** para una aplicación web. |
| **Permitir flujo implícito** | Sí | Seleccione **Sí** si su aplicación usa el [inicio de sesión de OpenID Connect](../articles/active-directory-b2c/active-directory-b2c-reference-oidc.md). |
| **URL de respuesta** | `https://localhost:44316` | Las direcciones URL de respuesta son puntos de conexión en los que Azure AD B2C devolverá los tokens que su aplicación solicite. Escriba una **dirección URL de respuesta** [adecuada](../articles/active-directory-b2c/active-directory-b2c-app-registration.md#choosing-a-web-app-or-api-reply-url). En este ejemplo, la aplicación es local y la escucha se realiza en el puerto 44316. |

Haga clic en **Crear** para registrar la aplicación.

La aplicación recién registrada aparece en la lista de aplicaciones del inquilino B2C. Seleccione la aplicación web en la lista. Se muestra el panel de propiedades de la aplicación web.

![Propiedades de la aplicación web](./media/active-directory-b2c-register-web-app/b2c-web-app-properties.png)

Tome nota del **Id. de cliente de aplicación** único. Use el identificador en el código de la aplicación.

