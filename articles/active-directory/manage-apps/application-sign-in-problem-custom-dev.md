---
title: Problemas de inicio de sesión en una aplicación desarrollada personalizada | Microsoft Docs
description: Errores comunes que pueden causar la imposibilidad de iniciar sesión en una aplicación desarrollada con Azure AD
services: active-directory
documentationcenter: ''
author: CelesteDG
manager: mtillman
ms.assetid: ''
ms.service: active-directory
ms.subservice: app-mgmt
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 07/11/2017
ms.author: celested
ms.reviewer: asteen
ms.collection: M365-identity-device-management
ms.openlocfilehash: f4365c87f0028fe3a9c4ba35f40599359eb1455f
ms.sourcegitcommit: 3102f886aa962842303c8753fe8fa5324a52834a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "60438785"
---
# <a name="problems-signing-in-to-an-custom-developed-application"></a>Problemas de inicio de sesión en una aplicación desarrollada personalizada

Hay varios errores que pueden provocar que no pueda iniciar sesión en una aplicación. El principal motivo por el que los usuarios encuentran este problema son las aplicaciones mal configuradas.

## <a name="errors-related-to--misconfigured-apps"></a>Errores relacionados con aplicaciones mal configuradas

* Compruebe que las configuraciones en el portal coinciden con lo que tiene en la aplicación. En concreto, compare el identificador del cliente o aplicación, las direcciones URL de respuesta, las claves y secretos de cliente, y el URI del identificador de la aplicación.

* Compare el recurso del que está solicitando acceso mediante código con los permisos configurados en la pestaña **Recursos necesarios** para asegurarse de que solo se solicitan los recursos que ha configurado.

* Busque en [Azure AD en StackOverflow](https://stackoverflow.com/questions/tagged/azure-active-directory) errores o problemas similares.

## <a name="next-steps"></a>Pasos siguientes

[Guía del desarrollador de Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-developers-guide)<br>

[Consentimiento e integración de aplicaciones en Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications)<br>

[Consentimiento y permisos para las aplicaciones convergentes v2.0 de Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes)<br>

[Azure AD en StackOverflow](https://stackoverflow.com/questions/tagged/azure-active-directory>)
