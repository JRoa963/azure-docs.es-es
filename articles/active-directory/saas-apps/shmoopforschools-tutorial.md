---
title: 'Tutorial: Integración de Azure Active Directory con Shmoop For Schools | Microsoft Docs'
description: Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Shmoop For Schools.
services: active-directory
documentationCenter: na
author: jeevansd
manager: daveba
ms.reviewer: joflore
ms.assetid: 1d75560a-55b3-42e9-bda1-92b01c572d8e
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/23/2018
ms.author: jeedes
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4091b20e97ca76629260a7420beecb77412b0d39
ms.sourcegitcommit: 3102f886aa962842303c8753fe8fa5324a52834a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "60310865"
---
# <a name="tutorial-azure-active-directory-integration-with-shmoop-for-schools"></a>Tutorial: Integración de Azure Active Directory con Shmoop For Schools

En este tutorial, obtendrá información sobre cómo integrar Shmoop For Schools con Azure Active Directory (Azure AD).

La integración de Shmoop For Schools con Azure AD proporciona las siguientes ventajas:

- Puede controlar en Azure AD quién tiene acceso a Shmoop For Schools.
- Puede permitir que los usuarios inicien sesión automáticamente en Shmoop For Schools con sus cuentas de Azure AD.
- Puede administrar sus cuentas en una ubicación central: Azure Portal.

Para más información sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Requisitos previos

Para configurar la integración de Azure AD con Shmoop For Schools, necesita los siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción a Shmoop For Schools con inicio de sesión único habilitado

> [!NOTE]
> Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.

Para probar los pasos en este tutorial, se recomienda:

- Uso de su entorno de producción solo si es necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede obtener una [versión de evaluación gratuita durante un mes](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba. La situación descrita en este tutorial consta de dos bloques de creación principales:

1. Adición de Shmoop For Schools desde la galería
2. Configuración y comprobación del inicio de sesión único de Azure AD

## <a name="add-shmoop-for-schools-from-the-gallery"></a>Adición de Shmoop For Schools desde la galería
Para configurar la integración de Shmoop For Schools en Azure AD, será preciso que agregue Shmoop For Schools desde la galería a la lista de aplicaciones SaaS administradas.

**Para agregar Shmoop For Schools desde la galería, siga estos pasos:**

1. En el panel izquierdo de [Azure Portal](https://portal.azure.com), seleccione el icono **Azure Active Directory**. 

    ![Botón Azure Active Directory][1]

2. Vaya a **Aplicaciones empresariales**. A continuación, vaya a **Todas las aplicaciones**.

    ![Hoja Aplicaciones empresariales][2]
    
3. Para agregar una nueva aplicación, seleccione el botón **Nueva aplicación** en la parte superior del cuadro de diálogo.

    ![Botón Nueva aplicación][3]

4. En el cuadro de búsqueda, escriba **Shmoop For Schools**. Seleccione **Shmoop For Schools** en los resultados y, luego, haga clic en el botón **Agregar** para agregar la aplicación.

    ![Shmoop For Schools en la lista de resultados](./media/shmoopforschools-tutorial/tutorial_shmoopforschools_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configuración y prueba del inicio de sesión único en Azure AD

En esta sección, se configura y se prueba el inicio de sesión único de Azure AD con Shmoop For Schools con un usuario de prueba llamado "Britta Simon".

Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Shmoop For Schools para un usuario de Azure AD. Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Shmoop For Schools.

Para configurar y probar el inicio de sesión único de Azure AD con Shmoop For Schools, tiene que completar los siguientes bloques de creación:

1. [Configuración del inicio de sesión único de Azure AD](#configure-azure-ad-single-sign-on), para permitir que los usuarios utilicen esta característica.
2. [Creación de un usuario de prueba de Azure AD](#create-an-azure-ad-test-user), para probar el inicio de sesión único de Azure AD con Britta Simon.
3. [Creación de un usuario de prueba de Shmoop For Schools](#create-a-shmoop-for-schools-test-user), para tener un homólogo de Britta Simon en Shmoop For Schools que esté vinculado a la representación del usuario en Azure AD.
4. [Asignación del usuario de prueba de Azure AD](#assign-the-azure-ad-test-user), para permitir que Britta Simon use el inicio de sesión único de Azure AD.
5. [Prueba del inicio de sesión único](#test-single-sign-on) para comprobar que la configuración funciona.

### <a name="configure-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en la aplicación Shmoop For Schools.

**Para configurar el inicio de sesión único de Azure AD con Shmoop For Schools, siga estos pasos:**

1. En la página de integración de la aplicación **Shmoop For Schools** de Azure Portal, seleccione **Inicio de sesión único**.

    ![Vínculo Configurar inicio de sesión único][4]

2. En el cuadro de diálogo **Inicio de sesión único**, en el menú desplegable en **Modo de inicio de sesión único**, seleccione **Inicio de sesión basado en SAML**.
 
    ![Cuadro de diálogo Inicio de sesión único](./media/shmoopforschools-tutorial/tutorial_shmoopforschools_samlbase.png)

3. En la sección **Dominio y direcciones URL de Shmoop For Schools**, lleve a cabo los pasos siguientes:

    ![Configurar inicio de sesión único](./media/shmoopforschools-tutorial/tutorial_shmoopforschools_url.png)

     a. En el cuadro **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://schools.shmoop.com/public-api/saml2/start/<uniqueid>`

    b. En el cuadro **Identificador**, escriba una dirección URL con el siguiente patrón: `https://schools.shmoop.com/<uniqueid>`

    > [!NOTE] 
    > Estos valores no son reales. Debe actualizarlos con la dirección URL de inicio de sesión y el identificador reales. Póngase en contacto con el [equipo de soporte de cliente de Shmoop For Schools](mailto:support@shmoop.com) para obtener estos valores. 
 
4. La aplicación Shmoop For Schools espera las aserciones de SAML en un formato específico. Configure las siguientes notificaciones para esta aplicación. Puede administrar los valores de estos atributos en la sección **Atributos de usuario** de la página de integración de aplicaciones. La captura de pantalla siguiente muestra cómo configurar las aserciones:

    ![Configurar inicio de sesión único](./media/shmoopforschools-tutorial/tutorial_attribute.png)

    > [!NOTE]
    > Shmoop For Schools admite dos roles para los usuarios: **Teacher** (Profesor) y **Student** (Alumno). Configure estos roles en Azure AD para que se pueda asignar a los usuarios los roles correspondientes. Para comprender cómo configurar roles en Azure AD, consulte [Administración del acceso mediante RBAC y Azure Portal](../../role-based-access-control/role-assignments-portal.md).
    
5. En la sección **Atributos de usuario** del cuadro de diálogo **Inicio de sesión único**, configure el atributo token SAML como muestra la imagen anterior.  A continuación, siga estos pasos:

    | Nombre del atributo | Valor de atributo |
    | -------------- | --------------- |
    | role           | user.assignedroles |

     a. Seleccione **Agregar atributo** para abrir el cuadro de diálogo **Agregar atributo**.
    
    ![Configurar inicio de sesión único](./media/shmoopforschools-tutorial/tutorial_attribute_04.png)
    
    ![Configurar inicio de sesión único](./media/shmoopforschools-tutorial/tutorial_attribute_05.png)
    
    b. En el cuadro **Nombre**, escriba el nombre del atributo que se muestra para esa fila.
    
    c. En la lista **Valor**, seleccione el valor del atributo que se muestra para esa fila.

    d. Deje **Espacio de nombres** vacío.
    
    e. Seleccione **Aceptar**.

6. Seleccione el botón **Guardar**.

    ![Configurar inicio de sesión único](./media/shmoopforschools-tutorial/tutorial_general_400.png)

7. En la sección **Certificado de firma de SAML** , haga clic en el botón Copiar para copiar la **dirección URL de metadatos de federación de la aplicación** y péguela en el Bloc de notas.

    ![Vínculo de descarga del certificado](./media/shmoopforschools-tutorial/tutorial_shmoopforschools_certificate.png)

8. Para configurar el inicio de sesión único en **Shmoop For Schools**, debe enviar la **dirección URL de metadatos de federación de la aplicación** al [equipo de soporte técnico de Shmoop For Schools](mailto:support@shmoop.com).

### <a name="create-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD

El objetivo de esta sección es crear un usuario de prueba llamado Britta Simon en Azure Portal.

   ![Creación de un usuario de prueba de Azure AD][100]

**Siga estos pasos para crear un usuario de prueba en Azure AD:**

1. En el panel izquierdo de Azure Portal, seleccione el botón **Azure Active Directory**.

    ![Botón Azure Active Directory](./media/shmoopforschools-tutorial/create_aaduser_01.png)

2. Para mostrar la lista de usuarios, vaya a **Usuarios y grupos**. Después, seleccione **Todos los usuarios**.

    ![Vínculos "Usuarios y grupos" y "Todos los usuarios"](./media/shmoopforschools-tutorial/create_aaduser_02.png)

3. En la parte superior del cuadro de diálogo **Todos los usuarios**, seleccione **Agregar** para abrir el cuadro de diálogo **Usuario**.

    ![Botón Agregar](./media/shmoopforschools-tutorial/create_aaduser_03.png)

4. En el cuadro de diálogo **Usuario**, realice los pasos siguientes:

    ![Cuadro de diálogo Usuario](./media/shmoopforschools-tutorial/create_aaduser_04.png)

     a. En el cuadro **Nombre**, escriba **BrittaSimon**.

    b. En el cuadro de texto **Nombre de usuario**, escriba la dirección de correo electrónico del usuario Britta Simon.

    c. Active la casilla **Mostrar contraseña** y, después, anote el valor que se muestra en el cuadro **Contraseña**.

    d. Seleccione **Crear**.
 
### <a name="create-a-shmoop-for-schools-test-user"></a>Creación de un usuario de prueba de Shmoop For Schools

El objetivo de esta sección es crear un usuario llamado Britta Simon en Shmoop For Schools. Shmoop For Schools admite el aprovisionamiento Just-In-Time, que está habilitado de forma predeterminada. No hay ningún elemento de acción para usted en esta sección. Si un nuevo usuario no existe, se crea durante el intento de obtener acceso a Shmoop For Schools.

>[!NOTE]
>Si necesita crear manualmente un usuario, póngase en contacto con el [equipo de soporte técnico de Shmoop For Schools](mailto:support@shmoop.com).

### <a name="assign-the-azure-ad-test-user"></a>Asignación del usuario de prueba de Azure AD

En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Shmoop For Schools.

![Asignación de rol de usuario][200] 

**Para asignar Britta Simon a Shmoop For Schools, realice los pasos siguientes:**

1. En Azure Portal, abra la vista de aplicaciones. A continuación, vaya a **Aplicaciones empresariales** en la vista de directorio.  A continuación, seleccione **Todas las aplicaciones**.

    ![Asignar usuario][201] 

2. En la lista de aplicaciones, seleccione **Shmoop For Schools**.

    ![Vínculo a Shmoop For Schools en la lista de aplicaciones](./media/shmoopforschools-tutorial/tutorial_shmoopforschools_app.png)  

3. En el menú de la izquierda, seleccione **Usuarios y grupos**.

    ![Vínculo "Usuarios y grupos"][202]

4. Seleccione el botón **Agregar**. Después, en el cuadro de diálogo **Agregar asignación**, seleccione **Usuarios y grupos**.

    ![Panel Agregar asignación][203]

5. En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon**.

6. En el cuadro de diálogo **Usuarios y grupos**, haga clic en el botón **Seleccionar**. 

7. En el cuadro de diálogo **Agregar asignación**, haga clic en el botón **Asignar**.
    
### <a name="test-single-sign-on"></a>Prueba de inicio de sesión único

En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.

Al seleccionar el icono **Shmoop For Schools** del panel de acceso, debería iniciar sesión automáticamente en la aplicación Shmoop For Schools.

Para más información sobre el Panel de acceso, consulte la [introducción al Panel de acceso](../user-help/active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory](tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/shmoopforschools-tutorial/tutorial_general_01.png
[2]: ./media/shmoopforschools-tutorial/tutorial_general_02.png
[3]: ./media/shmoopforschools-tutorial/tutorial_general_03.png
[4]: ./media/shmoopforschools-tutorial/tutorial_general_04.png

[100]: ./media/shmoopforschools-tutorial/tutorial_general_100.png

[200]: ./media/shmoopforschools-tutorial/tutorial_general_200.png
[201]: ./media/shmoopforschools-tutorial/tutorial_general_201.png
[202]: ./media/shmoopforschools-tutorial/tutorial_general_202.png
[203]: ./media/shmoopforschools-tutorial/tutorial_general_203.png

