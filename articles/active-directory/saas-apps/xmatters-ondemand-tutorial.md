---
title: 'Tutorial: Integración de Azure Active Directory con xMatters OnDemand | Microsoft Docs'
description: Aprenda a configurar el inicio de sesión único entre Azure Active Directory y xMatters OnDemand.
services: active-directory
documentationCenter: na
author: jeevansd
manager: daveba
ms.assetid: ca0633db-4f95-432e-b3db-0168193b5ce9
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2018
ms.author: jeedes
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8b5ec711f0e43d9d29d962d43ed8b1d86338db87
ms.sourcegitcommit: 61c8de2e95011c094af18fdf679d5efe5069197b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62114935"
---
# <a name="tutorial-azure-active-directory-integration-with-xmatters-ondemand"></a>Tutorial: Integración de Azure Active Directory con xMatters OnDemand

En este tutorial, aprenderá a integrar xMatters OnDemand con Azure Active Directory (Azure AD).

Integrar xMatters OnDemand con Azure AD proporciona las siguientes ventajas:

- Puede controlar en Azure AD quién tiene acceso a xMatters OnDemand.
- Puede permitir que los usuarios inicien sesión automáticamente en xMatters OnDemand (inicio de sesión único) con sus cuentas de Azure AD.
- Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.

Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Requisitos previos

Para configurar la integración de Azure AD con xMatters OnDemand, necesita los siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción habilitada para el inicio de sesión único en xMatters OnDemand

> [!NOTE]
> Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.

Para probar los pasos de este tutorial, debe seguir estas recomendaciones:

- No use el entorno de producción, salvo que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba. El escenario descrito en este tutorial consta de dos bloques de creación principales:

1. Incorporación de xMatters OnDemand desde la galería
1. Configuración y comprobación del inicio de sesión único de Azure AD

## <a name="adding-xmatters-ondemand-from-the-gallery"></a>Incorporación de xMatters OnDemand desde la galería
Para configurar la integración de xMatters OnDemand en Azure AD, deberá agregarlo desde la galería a la lista de aplicaciones SaaS administradas.

**Para agregar xMatters OnDemand desde la galería, realice los pasos siguientes:**

1. En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**. 

    ![Active Directory][1]

1. Vaya a **Aplicaciones empresariales**. A continuación, vaya a **Todas las aplicaciones**.

    ![APLICACIONES][2]
    
1. Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.

    ![APLICACIONES][3]

1. En el cuadro de búsqueda, escriba **xMatters OnDemand**.

    ![Creación de un usuario de prueba de Azure AD](./media/xmatters-ondemand-tutorial/tutorial_xmattersondemand_search.png)

1. En el panel de resultados, seleccione **xMatters OnDemand** y, luego, haga clic en el botón **Agregar** para agregar la aplicación.

    ![Creación de un usuario de prueba de Azure AD](./media/xmatters-ondemand-tutorial/tutorial_xmattersondemand_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuración y comprobación del inicio de sesión único de Azure AD
En esta sección, va a configurar y probar el inicio de sesión único de Azure AD con xMatters OnDemand con un usuario de prueba llamado "Britta Simon".

Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de xMatters OnDemand para un usuario de Azure AD. Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de xMatters OnDemand.

Para establecer la relación de vínculo, en xMatters OnDemand, asigne el valor del **nombre de usuario** en Azure AD como el valor del **nombre de usuario**.

Para configurar y probar el inicio de sesión único de Azure AD con xMatters OnDemand, es preciso completar los siguientes bloques de creación:

1. **[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.
1. **[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.
1. **[Creación de un usuario de prueba de xMatters OnDemand](#creating-a-xmatters-ondemand-test-user)**: para tener un homólogo de Britta Simon en xMatters OnDemand que esté vinculado a la representación de Azure AD del usuario.
1. **[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.
1. **[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación xMatters OnDemand.

**Para configurar el inicio de sesión único de Azure AD con xMatters OnDemand, realice los pasos siguientes:**

1. En Azure Portal, en la página de integración de la aplicación **xMatters OnDemand**, haga clic en **Inicio de sesión único**.

    ![Configurar inicio de sesión único][4]

1. En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.

    ![Configurar inicio de sesión único](./media/xmatters-ondemand-tutorial/tutorial_xmattersondemand_samlbase.png)

1. En la sección **Dominio y direcciones URL de xMatters OnDemand**, lleve a cabo los pasos siguientes:

    ![Configurar inicio de sesión único](./media/xmatters-ondemand-tutorial/tutorial_xmattersondemand_url.png)
    
     a. En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón:

    | |
    |--|
    | `https://<companyname>.au1.xmatters.com.au/`|
    | `https://<companyname>.cs1.xmatters.com/`|
    | `https://<companyname>.xmatters.com/`|
    | `https://www.xmatters.com`|
    | `https://<companyname>.xmatters.com.au/`|

    b. En el cuadro de texto **URL de respuesta** , escriba una dirección URL con el siguiente patrón:
    
    | |
    |--|
    | `https://<companyname>.au1.xmatters.com.au`|
    | `https://<companyname>.xmatters.com/sp/<instancename>`|
    | `https://<companyname>.cs1.xmatters.com/sp/<instancename>`|
    | `https://<companyname>.au1.xmatters.com.au/<instancename>`|

    > [!NOTE] 
    > Estos valores no son reales. Actualice estos valores con el identificador y la URL de respuesta reales. Póngase en contacto con el [equipo de soporte técnico de xMatters OnDemand](https://www.xmatters.com/company/contact-us/) para obtener estos valores.

1. En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado localmente en **c:\\XMatters OnDemand.cer**.

    ![Configurar inicio de sesión único](./media/xmatters-ondemand-tutorial/tutorial_xmattersondemand_certificate.png)

    > [!IMPORTANT]
    > Debe reenviar el certificado al [equipo de soporte técnico de xMatters OnDemand](https://www.xmatters.com/company/contact-us/). El equipo de soporte técnico de xMatters debe cargar el certificado para que se pueda finalizar la configuración del inicio de sesión único. 

1. Haga clic en el botón **Guardar** .

    ![Configurar inicio de sesión único](./media/xmatters-ondemand-tutorial/tutorial_general_400.png)

1. En la sección **Configuración de xMatters OnDemand**, haga clic en **Configurar xMatters OnDemand** para abrir la ventana **Configurar inicio de sesión**. Copie la **URL del servicio de inicio de sesión único de SAML, el identificador de entidad de SAML y la dirección URL de cierre de sesión** de la sección **Referencia rápida**.

    ![Configurar inicio de sesión único](./media/xmatters-ondemand-tutorial/tutorial_xmattersondemand_configure.png) 

1. En otra ventana del explorador web, inicie sesión en el sitio de la compañía de xMatters OnDemand como administrador.

1. En la barra de herramientas de la parte superior, haga clic en **Administrador** y luego en **Detalles de la compañía** en la barra de navegación del lado izquierdo.

    ![Administración](./media/xmatters-ondemand-tutorial/IC776795.png "Administración")

1. En la página **Configuración de SAML** , realice los siguientes pasos:

    ![Configuración de SAML](./media/xmatters-ondemand-tutorial/IC776796.png "Configuración de SAML")

     a. Seleccione **Habilitar SAML**.

    b. En el cuadro de texto **Identity Provider ID** (Identificador del proveedor de identidad), pegue el valor de **SAML Entity ID** (Identificador de entidad de SAML) que ha copiado de Azure Portal.

    c. En el cuadro de texto **Single Sign-On URL** (Dirección URL de inicio de sesión único), pegue el valor de **SAML Single Sign-On Service URL** (Dirección URL del servicio de inicio de sesión único de SAML) que ha copiado de Azure Portal.

    d. En el cuadro de texto **Dirección URL de cierre de sesión único**, pegue el valor de **Dirección URL de cierre de sesión** que ha copiado de Azure Portal.

    e. En la página de detalles de la compañía, en la parte superior, haga clic en **Guardar cambios**.

    ![Detalles de la compañía](./media/xmatters-ondemand-tutorial/IC776797.png "Detalles de la compañía")

### <a name="creating-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".

![Creación de un usuario de Azure AD][100]

**Siga estos pasos para crear un usuario de prueba en Azure AD:**

1. En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.

    ![Creación de un usuario de prueba de Azure AD](./media/xmatters-ondemand-tutorial/create_aaduser_01.png) 

1. Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.

    ![Creación de un usuario de prueba de Azure AD](./media/xmatters-ondemand-tutorial/create_aaduser_02.png) 

1. Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.

    ![Creación de un usuario de prueba de Azure AD](./media/xmatters-ondemand-tutorial/create_aaduser_03.png) 

1. En la página de diálogo **Usuario**, realice los siguientes pasos:

    ![Creación de un usuario de prueba de Azure AD](./media/xmatters-ondemand-tutorial/create_aaduser_04.png) 

     a. En el cuadro de texto **Nombre**, escriba **BrittaSimon**.

    b. En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.

    c. Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.

    d. Haga clic en **Create**(Crear).

### <a name="creating-a-xmatters-ondemand-test-user"></a>Creación de un usuario de prueba de xMatters OnDemand

El objetivo de esta sección es crear un usuario de prueba llamado Britta Simon en xMatters OnDemand.

**Para crear un usuario manualmente, siga los pasos siguientes:**

1. Inicie sesión en su inquilino de **xMatters OnDemand** .

1. Haga clic en la pestaña **Users** (Usuarios) y, luego, en **Add User** (Agregar usuario).

   ![Usuarios](./media/xmatters-ondemand-tutorial/IC781048.png "Usuarios")

1. En la sección **Agregar un usuario** , realice estos pasos:

    ![Agregar un usuario](./media/xmatters-ondemand-tutorial/IC781049.png "Agregar un usuario")

     a. Seleccione **Active**(Activo).

    b. En el cuadro de texto **User ID** (Identificador de usuario), escriba el identificador de usuario, en este caso, Brittasimon@contoso.com.

    c. En el cuadro de texto **Nombre**, escriba el nombre del usuario, en este caso, Britta.

    d. En el cuadro de texto **Apellidos**, escriba el apellido del usuario, en este caso Simon.

    e. En el cuadro de texto **Sitio**, escriba el sitio válido de una cuenta de Azure AD válida que quiera aprovisionar.

    f. Haga clic en **Save**(Guardar).

### <a name="assigning-the-azure-ad-test-user"></a>Asignación del usuario de prueba de Azure AD

En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a xMatters OnDemand.

![Asignar usuario][200] 

**Para asignar a Britta Simon a xMatters OnDemand, lleve a cabo los pasos siguientes:**

1. En Azure Portal, abra la vista de aplicaciones, navegue a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego haga clic en **Todas las aplicaciones**.

    ![Asignar usuario][201] 

1. En la lista de aplicaciones, seleccione  **xMatters OnDemand**.

    ![Configurar inicio de sesión único](./media/xmatters-ondemand-tutorial/tutorial_xmattersondemand_app.png) 

1. En el menú de la izquierda, haga clic en **Usuarios y grupos**.

    ![Asignar usuario][202] 

1. Haga clic en el botón **Agregar**. Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.

    ![Asignar usuario][203]

1. En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.

1. Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.

1. Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.
    
### <a name="testing-single-sign-on"></a>Prueba del inicio de sesión único 

En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.

Al hacer clic en el icono de xMatters OnDemand en el panel de acceso, debería iniciar sesión automáticamente en la aplicación xMatters OnDemand.
Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](../user-help/active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory](tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/xmatters-ondemand-tutorial/tutorial_general_01.png
[2]: ./media/xmatters-ondemand-tutorial/tutorial_general_02.png
[3]: ./media/xmatters-ondemand-tutorial/tutorial_general_03.png
[4]: ./media/xmatters-ondemand-tutorial/tutorial_general_04.png

[100]: ./media/xmatters-ondemand-tutorial/tutorial_general_100.png

[200]: ./media/xmatters-ondemand-tutorial/tutorial_general_200.png
[201]: ./media/xmatters-ondemand-tutorial/tutorial_general_201.png
[202]: ./media/xmatters-ondemand-tutorial/tutorial_general_202.png
[203]: ./media/xmatters-ondemand-tutorial/tutorial_general_203.png
