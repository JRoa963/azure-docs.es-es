---
title: Almacenamiento de objetos (Blob Storage) de Xamarin | Microsoft Docs
description: La biblioteca cliente de Azure Storage para Xamarin permite a los desarrolladores crear aplicaciones iOS, Android y de la Tienda Windows con sus interfaces de usuario nativas. Este tutorial muestra cómo usar Xamarin para crear una aplicación Android que usa Azure Blob Storage.
services: storage
documentationcenter: xamarin
author: mhopkins-msft
ms.service: storage
ms.topic: article
ms.date: 05/11/2017
ms.author: mhopkins
ms.reviewer: seguler
ms.openlocfilehash: 1953a0af89e5ea018bd3654c3b82087331b3d565
ms.sourcegitcommit: f6ba5c5a4b1ec4e35c41a4e799fb669ad5099522
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/06/2019
ms.locfileid: "65141278"
---
# <a name="how-to-use-blob-storage-from-xamarin"></a>Uso de Blob Storage desde Xamarin

Xamarin permite a los desarrolladores usar un código base C# compartida para crear aplicaciones de iOS, Android y de la Tienda Windows con sus interfaces de usuario nativas. En este tutorial se muestra cómo usar Azure Blob Storage con una aplicación de Xamarin. Si desea más información sobre Azure Storage, antes de entrar en el código, consulte [Introducción a Microsoft Azure Storage](../common/storage-introduction.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-mobile-authentication-guidance](../../../includes/storage-mobile-authentication-guidance.md)]

## <a name="create-a-new-xamarin-application"></a>Creación de una nueva aplicación Xamarin
En este tutorial, crearemos una aplicación destinada a Android, iOS y Windows. Esta aplicación creará simplemente un contenedor y cargará un blob en este contenedor. Aunque vamos a usar Visual Studio en Windows, se pueden aplicar los mismos conocimientos al crear una aplicación mediante Xamarin Studio en Mac OS.

Para crear la aplicación, siga estos pasos:

1. Si aún no lo ha hecho, descargue e instale o [Xamarin para Visual Studio](https://www.xamarin.com/download).
2. Abra Visual Studio y cree una aplicación en blanco (nativa portátil): **Archivo > Nuevo > proyecto > multiplataforma > Blank App (Native Portable)**.
3. Haga clic con el botón derecho en la solución en el panel del Explorador de soluciones y seleccione **Administrar paquetes NuGet para la solución**. Busque **WindowsAzure.Storage** e instale la versión estable más reciente para todos los proyectos de su solución.
4. Compile y ejecute el proyecto.

Ahora debería tener una aplicación que le permita hacer clic en un botón e incrementar un contador.

## <a name="create-container-and-upload-blob"></a>Creación de un contenedor y carga de un blob
Después, en su proyecto `(Portable)`, agregará código a `MyClass.cs`. Este código crea un contenedor y carga un blob en dicho contenedor. `MyClass.cs` debería ser similar al siguiente:

```csharp
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
using System.Threading.Tasks;

namespace XamarinApp
{
    public class MyClass
    {
        public MyClass ()
        {
        }

        public static async Task performBlobOperation()
        {
            // Retrieve storage account from connection string.
            CloudStorageAccount storageAccount = CloudStorageAccount.Parse("DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here");

            // Create the blob client.
            CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

            // Retrieve reference to a previously created container.
            CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

            // Create the container if it doesn't already exist.
            await container.CreateIfNotExistsAsync();

            // Retrieve reference to a blob named "myblob".
            CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

            // Create the "myblob" blob with the text "Hello, world!"
            await blockBlob.UploadTextAsync("Hello, world!");
        }
    }
}
```

Asegúrese de reemplazar "su_nombre_de_cuenta_aquí" y "su_clave_de_cuenta_aquí" por el nombre de cuenta y la clave de cuenta reales. 

Todos los proyectos para iOS, Android y Windows Phone tienen referencias al proyecto portátil, lo que significa que puede escribir todo su código compartido en un lugar y utilizarlo en todos los proyectos. Ahora puede agregar la siguiente línea de código a cada proyecto para empezar a aprovechar: `MyClass.performBlobOperation()`

### <a name="xamarinappdroid--mainactivitycs"></a>XamarinApp.Droid > MainActivity.cs

```csharp
using Android.App;
using Android.Widget;
using Android.OS;

namespace XamarinApp.Droid
{
    [Activity (Label = "XamarinApp.Droid", MainLauncher = true, Icon = "@drawable/icon")]
    public class MainActivity : Activity
    {
        int count = 1;

        protected override async void OnCreate (Bundle bundle)
        {
            base.OnCreate (bundle);

            // Set our view from the "main" layout resource
            SetContentView (Resource.Layout.Main);

            // Get our button from the layout resource,
            // and attach an event to it
            Button button = FindViewById<Button> (Resource.Id.myButton);

            button.Click += delegate {
                button.Text = string.Format ("{0} clicks!", count++);
            };

            await MyClass.performBlobOperation();
            }
        }
    }
}
```

### <a name="xamarinappios--viewcontrollercs"></a>XamarinApp.iOS > ViewController.cs

```csharp
using System;
using UIKit;

namespace XamarinApp.iOS
{
    public partial class ViewController : UIViewController
    {
        int count = 1;

        public ViewController (IntPtr handle) : base (handle)
        {
        }

        public override async void ViewDidLoad ()
        {
            int count = 1;

            public ViewController (IntPtr handle) : base (handle)
            {
            }

            public override async void ViewDidLoad ()
            {
                base.ViewDidLoad ();
                // Perform any additional setup after loading the view, typically from a nib.
                Button.AccessibilityIdentifier = "myButton";
                Button.TouchUpInside += delegate {
                    var title = string.Format ("{0} clicks!", count++);
                    Button.SetTitle (title, UIControlState.Normal);
                };

                await MyClass.performBlobOperation();
            }

            public override void DidReceiveMemoryWarning ()
            {
                base.DidReceiveMemoryWarning ();
                // Release any cached data, images, etc. that aren't in use.
            }
        }
    }
}
```

### <a name="xamarinappwinphone--mainpagexaml--mainpagexamlcs"></a>XamarinApp.WinPhone > MainPage.xaml > MainPage.xaml.cs

```csharp
using Windows.UI.Xaml.Controls;
using Windows.UI.Xaml.Navigation;

// The Blank Page item template is documented at https://go.microsoft.com/fwlink/?LinkId=391641

namespace XamarinApp.WinPhone
{
    /// <summary>
    /// An empty page that can be used on its own or navigated to within a Frame.
    /// </summary>
    public sealed partial class MainPage : Page
    {
        int count = 1;

        public MainPage()
        {
            this.InitializeComponent();

            this.NavigationCacheMode = NavigationCacheMode.Required;
        }

        /// <summary>
        /// Invoked when this page is about to be displayed in a Frame.
        /// </summary>
        /// <param name="e">Event data that describes how this page was reached.
        /// This parameter is typically used to configure the page.</param>
        protected override async void OnNavigatedTo(NavigationEventArgs e)
        {
            int count = 1;

            public MainPage()
            {
                this.InitializeComponent();

                this.NavigationCacheMode = NavigationCacheMode.Required;
            }

            /// <summary>
            /// Invoked when this page is about to be displayed in a Frame.
            /// </summary>
            /// <param name="e">Event data that describes how this page was reached.
            /// This parameter is typically used to configure the page.</param>
            protected override async void OnNavigatedTo(NavigationEventArgs e)
            {
                // TODO: Prepare page for display here.

                // TODO: If your application contains multiple pages, ensure that you are
                // handling the hardware Back button by registering for the
                // Windows.Phone.UI.Input.HardwareButtons.BackPressed event.
                // If you are using the NavigationHelper provided by some templates,
                // this event is handled for you.
                Button.Click += delegate {
                    var title = string.Format("{0} clicks!", count++);
                    Button.Content = title;
                };

                await MyClass.performBlobOperation();
            }
        }
    }
}
```

## <a name="run-the-application"></a>Ejecución de la aplicación
Ahora puede ejecutar esta aplicación en un emulador Android o Windows Phone. También puede ejecutar esta aplicación en un emulador de iOS, pero necesitará un equipo Mac. Para obtener instrucciones específicas al respecto, lea la documentación sobre [cómo conectar Visual Studio con un equipo Mac](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/connecting-to-mac/)

Después de ejecutar su aplicación, se creará el contenedor `mycontainer` en su cuenta de Storage. Contendrá el blob `myblob`, que tiene el texto `Hello, world!`. Para comprobar esto, use el [Explorador de Microsoft Azure Storage](https://storageexplorer.com/).

## <a name="next-steps"></a>Pasos siguientes
En este tutorial, aprendió a crear una aplicación multiplataforma en Xamarin que usa Azure Storage, centrándose específicamente en un escenario en Blob Storage. Pero se puede hacer mucho más no solo con Blob Storage, sino también con Table, File y Queue Storage. Consulte los artículos siguientes para más información:

* [Introducción al Almacenamiento de blobs de Azure mediante .NET](storage-dotnet-how-to-use-blobs.md)
* [Introducción a Azure Files](../files/storage-files-introduction.md)
* [Desarrollo para Azure Files con .NET](../files/storage-dotnet-how-to-use-files.md)
* [Introducción al Almacenamiento de tablas de Azure mediante .NET](../../cosmos-db/table-storage-how-to-use-dotnet.md)
* [Introducción al Almacenamiento en cola de Azure mediante .NET](../queues/storage-dotnet-how-to-use-queues.md)

[!INCLUDE [storage-try-azure-tools-blobs](../../../includes/storage-try-azure-tools-blobs.md)]