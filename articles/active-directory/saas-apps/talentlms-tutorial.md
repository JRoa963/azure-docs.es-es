---
title: 'Tutorial: Integración de Azure Active Directory con TalentLMS | Microsoft Docs'
description: Aprenda a configurar el inicio de sesión único entre Azure Active Directory y TalentLMS.
services: active-directory
documentationCenter: na
author: jeevansd
manager: daveba
ms.assetid: c903d20d-18e3-42b0-b997-6349c5412dde
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: jeedes
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8fa78ec2b5623dfd010a8fe5709916a47e221a9e
ms.sourcegitcommit: 3102f886aa962842303c8753fe8fa5324a52834a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "60732337"
---
# <a name="tutorial-azure-active-directory-integration-with-talentlms"></a>Tutorial: Integración de Azure Active Directory con TalentLMS

En este tutorial, aprenderá a integrar TalentLMS con Azure Active Directory (Azure AD).

Integrar TalentLMS con Azure AD proporciona las siguientes ventajas:

- En Azure AD se puede controlar quién tiene acceso a TalentLMS
- Puede permitir que los usuarios inicien sesión automáticamente en TalentLMS (inicio de sesión único) con sus cuentas de Azure AD.
- Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.

Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Requisitos previos

Para configurar la integración de Azure AD con TalentLMS, necesita los siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción habilitada para el inicio de sesión único en TalentLMS

> [!NOTE]
> Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.

Para probar los pasos de este tutorial, debe seguir estas recomendaciones:

- No use el entorno de producción, salvo que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de evaluación de un mes aquí: [Oferta de evaluación](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba. El escenario descrito en este tutorial consta de dos bloques de creación principales:

1. Incorporación de TalentLMS desde la galería
1. Configuración y comprobación del inicio de sesión único de Azure AD

## <a name="adding-talentlms-from-the-gallery"></a>Incorporación de TalentLMS desde la galería
Para configurar la integración de TalentLMS en Azure AD, deberá agregar TalentLMS desde la galería a la lista de aplicaciones SaaS administradas.

**Para agregar TalentLMS desde la galería, siga estos pasos:**

1. En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**. 

    ![Active Directory][1]

1. Vaya a **Aplicaciones empresariales**. A continuación, vaya a **Todas las aplicaciones**.

    ![APLICACIONES][2]
    
1. Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.

    ![APLICACIONES][3]

1. En el cuadro de búsqueda, escriba **TalentLMS**.

    ![Creación de un usuario de prueba de Azure AD](./media/talentlms-tutorial/tutorial_talentlms_search.png)

1. En el panel de resultados, seleccione **TalentLMS** y, luego, haga clic en el botón **Agregar** para agregar la aplicación.

    ![Creación de un usuario de prueba de Azure AD](./media/talentlms-tutorial/tutorial_talentlms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuración y comprobación del inicio de sesión único de Azure AD
En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con TalentLMS con un usuario de prueba llamado "Britta Simon".

Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de TalentLMS para un usuario de Azure AD. Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de TalentLMS.

Para establecer la relación de vínculo, en TalentLMS, asigne el valor del **nombre de usuario** en Azure AD como el valor del **nombre de usuario**.

Para configurar y probar el inicio de sesión único de Azure AD con TalentLMS, es preciso completar los siguientes bloques de creación:

1. **[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.
1. **[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.
1. **[Creación de un usuario de prueba de TalentLMS](#creating-a-talentlms-test-user)**: para tener un homólogo de Britta Simon en TalentLMS que esté vinculado a la representación del usuario en Azure AD.
1. **[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.
1. **[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en la aplicación TalentLMS.

**Para configurar el inicio de sesión único de Azure AD con TalentLMS, realice los pasos siguientes:**

1. En Azure Portal, en la página de integración de la aplicación **TalentLMS**, haga clic en **Inicio de sesión único**.

    ![Configurar inicio de sesión único][4]

1. En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.
 
    ![Configurar inicio de sesión único](./media/talentlms-tutorial/tutorial_talentlms_samlbase.png)

1. En la sección **Dominio y direcciones URL de TalentLMS**, lleve a cabo los pasos siguientes:

    ![Configurar inicio de sesión único](./media/talentlms-tutorial/tutorial_talentlms_url.png)

     a. En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<tenant-name>.TalentLMSapp.com`.

    b. En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `http://<tenant-name>.talentlms.com`

    > [!NOTE] 
    > Estos valores no son reales. Debe actualizarlos con la dirección URL y el identificador reales de inicio de sesión. Póngase en contacto con el [equipo de soporte técnico de TalentLMS](https://www.talentlms.com/contact) para obtener estos valores. 
 
1. En la sección **Certificado de firma de SAML**, copie el valor de **HUELLA DIGITAL** del certificado.

    ![Configurar inicio de sesión único](./media/talentlms-tutorial/tutorial_talentlms_certificate.png) 

1. Haga clic en el botón **Guardar** .

    ![Configurar inicio de sesión único](./media/talentlms-tutorial/tutorial_general_400.png)

1. En la sección **Configuración de TalentLMS**, haga clic en **Configurar TalentLMS** para abrir la ventana **Configurar inicio de sesión**. Copie la **URL del servicio de inicio de sesión único de SAML, el identificador de entidad de SAML y la dirección URL de cierre de sesión** de la sección **Referencia rápida**.

    ![Configurar inicio de sesión único](./media/talentlms-tutorial/tutorial_talentlms_configure.png)  

1. En otra ventana del explorador web, inicie sesión en el sitio de la compañía de TalentLMS como administrador.

1. En la sección **Account & Settings** (Cuenta y configuración), haga clic en la pestaña **Users** (Usuarios).
   
    ![Cuenta y configuración](./media/talentlms-tutorial/IC777296.png "Cuenta y configuración")

1. Haga clic en **Inicio de sesión único (SSO)**.

1. En la sección Inicio de sesión único, siga estos pasos:
   
    ![Inicio de sesión único](./media/talentlms-tutorial/IC777297.png "Inicio de sesión único")   

     a. En la lista **SSO integration type** (Tipo de integración de SSO), seleccione **SAML 2.0**.

    b. En el cuadro de texto **Identity provider (IDP)** (Proveedor de identidad [IDP]), pegue el valor del **identificador de entidad de SAML** que ha copiado de Azure Portal.
 
    c. Pegue el valor de **Huella digital** de Azure Portal en el cuadro de texto de **Certificate fingerprint** (Huella digital de certificado).    

    d.  En el cuadro de texto **Remote sign-in URL** (Dirección URL de inicio de sesión remoto), pegue el valor de la **dirección URL de servicio de inicio de sesión único de SAML** que ha copiado de Azure Portal.
 
    e. En el cuadro de texto **Remote Log Out URL** (Dirección URL de cierre de sesión remoto), pegue el valor de **dirección URL de cierre de sesión** que copió de Azure Portal.

    f. Rellene lo siguiente: 

    * En el cuadro de texto **TargetedID** (Id. dirigido), escriba `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.
     
    * En el cuadro de texto **First name** (Nombre), escriba `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.
    
    * En el cuadro de texto **Last name** (Apellidos), escriba `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.
    
    * En el cuadro de texto **Email** (Correo electrónico), escriba `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.
    
1. Haga clic en **Save**(Guardar).
 
> [!TIP]
> Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.  Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior. Puede leer más aquí sobre la característica de documentación insertada: [Documentación insertada de Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".

![Creación de un usuario de Azure AD][100]

**Siga estos pasos para crear un usuario de prueba en Azure AD:**

1. En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.

    ![Creación de un usuario de prueba de Azure AD](./media/talentlms-tutorial/create_aaduser_01.png) 

1. Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.
    
    ![Creación de un usuario de prueba de Azure AD](./media/talentlms-tutorial/create_aaduser_02.png) 

1. Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.
 
    ![Creación de un usuario de prueba de Azure AD](./media/talentlms-tutorial/create_aaduser_03.png) 

1. En la página de diálogo **Usuario**, realice los siguientes pasos:
 
    ![Creación de un usuario de prueba de Azure AD](./media/talentlms-tutorial/create_aaduser_04.png) 

     a. En el cuadro de texto **Nombre**, escriba **BrittaSimon**.

    b. En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.

    c. Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.

    d. Haga clic en **Create**(Crear).
 
### <a name="creating-a-talentlms-test-user"></a>Creación de un usuario de prueba de TalentLMS

Para permitir que los usuarios de Azure AD inicien sesión en TalentLMS, deben aprovisionarse en TalentLMS. En el caso de TalentLMS, el aprovisionamiento es una tarea manual.

**Para aprovisionar una cuenta de usuario, realice estos pasos:**

1. Inicie sesión en su inquilino de **TalentLMS** .

1. Haga clic en **Users** (Usuarios) y, luego, en **Add User** (Agregar usuario).

1. En la página del cuadro de diálogo **Agregar usuario** , realice los siguientes pasos:
   
    ![Agregar usuario](./media/talentlms-tutorial/IC777299.png "Agregar usuario")  

     a. En el cuadro de texto **Nombre**, escriba el nombre de usuario, en este caso **Britta**.

    b. En el cuadro de texto **Apellidos**, escriba el apellido del usuario, en este caso **Simon**.
 
    c. En el cuadro de texto **Email address** (Dirección de correo electrónico), escriba la dirección de correo electrónico de un usuario, por ejemplo, **brittasimon\@contoso.com**.

    d. Haga clic en **Agregar usuario**.

>[!NOTE]
>Puede usar cualquier otra API o herramienta de creación de cuentas de usuario de TalentLMS ofrecida por TalentLMS para aprovisionar cuentas de usuario de AAD.
 

### <a name="assigning-the-azure-ad-test-user"></a>Asignación del usuario de prueba de Azure AD

En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a TalentLMS.

![Asignar usuario][200] 

**Para asignar Britta Simon a TalentLMS, realice los pasos siguientes:**

1. En Azure Portal, abra la vista de aplicaciones, navegue a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego haga clic en **Todas las aplicaciones**.

    ![Asignar usuario][201] 

1. En la lista de aplicaciones, seleccione **TalentLMS**.

    ![Configurar inicio de sesión único](./media/talentlms-tutorial/tutorial_talentlms_app.png) 

1. En el menú de la izquierda, haga clic en **Usuarios y grupos**.

    ![Asignar usuario][202] 

1. Haga clic en el botón **Agregar**. Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.

    ![Asignar usuario][203]

1. En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.

1. Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.

1. Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.
    
### <a name="testing-single-sign-on"></a>Prueba del inicio de sesión único 

El objetivo de esta sección es probar la configuración del inicio de sesión único de Azure AD mediante el panel de acceso.

Al hacer clic en el icono de TalentLMS en el panel de acceso, debería iniciar sesión automáticamente en su aplicación TalentLMS.

## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory](tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/talentlms-tutorial/tutorial_general_01.png
[2]: ./media/talentlms-tutorial/tutorial_general_02.png
[3]: ./media/talentlms-tutorial/tutorial_general_03.png
[4]: ./media/talentlms-tutorial/tutorial_general_04.png

[100]: ./media/talentlms-tutorial/tutorial_general_100.png

[200]: ./media/talentlms-tutorial/tutorial_general_200.png
[201]: ./media/talentlms-tutorial/tutorial_general_201.png
[202]: ./media/talentlms-tutorial/tutorial_general_202.png
[203]: ./media/talentlms-tutorial/tutorial_general_203.png

