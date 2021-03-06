---
title: Agregar una capa de símbolos para Android se asigna en Azure Maps | Microsoft Docs
description: Cómo agregar símbolos a un mapa mediante el SDK de Android de Azure Maps
author: walsehgal
ms.author: v-musehg
ms.date: 04/26/2019
ms.topic: conceptual
ms.service: azure-maps
services: azure-maps
manager: philmea
ms.openlocfilehash: add6e23d023753e217c102dc946837a71a64c781
ms.sourcegitcommit: e7d4881105ef17e6f10e8e11043a31262cfcf3b7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/29/2019
ms.locfileid: "64871083"
---
# <a name="add-a-symbol-layer-to-a-map-using-azure-maps-android-sdk"></a>Agregar una capa de símbolo a un mapa mediante el SDK de Android de Azure Maps

Este artículo muestra cómo representar el punto de datos desde un origen de datos como una capa de símbolos en un mapa mediante el SDK de Android de Azure Maps.

## <a name="prerequisites"></a>Requisitos previos

Para seguir completamente los pasos descritos en este artículo, necesitará instalar [Android SDK de Azure Maps](https://docs.microsoft.com/azure/azure-maps/how-to-use-android-map-control-library) para cargar un mapa.

## <a name="add-a-symbol-layer"></a>Adición de una capa de símbolo

Para agregar un marcador en un mapa mediante la capa de símbolos, siga estos pasos:

1. Editar **res** > **diseño** > **activity_main.xml** para que aparezca el siguiente código XML:
    
    ```XML
    <?xml version="1.0" encoding="utf-8"?>
    <FrameLayout
        xmlns:android="http://schemas.android.com/apk/res/android"
        xmlns:app="http://schemas.android.com/apk/res-auto"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        >

        <com.microsoft.azure.maps.mapcontrol.MapControl
            android:id="@+id/mapcontrol"
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            app:mapcontrol_centerLat="47.64"
            app:mapcontrol_centerLng="-122.33"
            app:mapcontrol_zoom="12"
            />

    </FrameLayout>
    ```

2. Copie el siguiente fragmento de código en el **onCreate()** método de su `MainActivity.java` clase.

    ```Java
    mapControl.onReady(map -> {
    
        //Create a data source and add it to the map.
        DataSource dataSource = new DataSource();
        map.sources.add(dataSource);
    
        //Create a point feature and add it to the data source.
        dataSource.add(Feature.fromGeometry(Point.fromLngLat(-122.33, 47.64)));
    
        //Add a custom image icon to the map resources.
        map.images.add("my-icon", R.drawable.mapcontrol_marker_red);
    
        //Create a symbol layer and add it to the map.
        map.layers.add(new SymbolLayer(dataSource,
            iconImage("my-icon")));
        });
    
    ```
    
    En primer lugar, el fragmento de código anterior obtiene un Azure Maps map control de instancias utilizando el **onReady()** método de devolución de llamada. A continuación, crea un objeto de origen de datos mediante el **DataSource** clase y lo agrega al mapa. A continuación, agrega un **característica** que contiene un objeto geometry de punto a él. A continuación, se establece una imagen de marcador rojo como icono para el símbolo. Un **capa símbolo** usa texto o iconos para representar encapsulados en el origen de datos como símbolos en el mapa de datos basada en punto. A continuación, se crea una capa de símbolo y el origen de datos se pasa a la que se va a representar y, a continuación, se agrega a las capas del mapa.
    
    Después de agregar el fragmento de código anterior, su `MainActivity.java` debería ser similar a lo siguiente:
    
    ```Java
    package com.example.myapplication;
    
    import android.app.Activity;
    import android.os.Bundle;
    import com.mapbox.geojson.Feature;
    import com.mapbox.geojson.Point;
    import com.microsoft.azure.maps.mapcontrol.AzureMaps;
    import com.microsoft.azure.maps.mapcontrol.MapControl;
    import com.microsoft.azure.maps.mapcontrol.layer.SymbolLayer;
    import com.microsoft.azure.maps.mapcontrol.source.DataSource;
    import static com.microsoft.azure.maps.mapcontrol.options.SymbolLayerOptions.iconImage;
    public class MainActivity extends AppCompatActivity {
        
        static{
                AzureMaps.setSubscriptionKey("<Your Azure Maps subscription key>");
            }
    
        MapControl mapControl;
        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
    
            mapControl = findViewById(R.id.mapcontrol);
    
            mapControl.onCreate(savedInstanceState);
    
            mapControl.onReady(map -> {
    
                //Create a data source and add it to the map.
                DataSource dataSource = new DataSource();
                map.sources.add(dataSource);
            
                //Create a point feature and add it to the data source.
                dataSource.add(Feature.fromGeometry(Point.fromLngLat(-122.33, 47.64)));
            
                //Add a custom image icon to the map resources.
                map.images.add("my-icon", R.drawable.mapcontrol_marker_red);
            
                //Create a symbol layer and add it to the map.
                map.layers.add(new SymbolLayer(dataSource,
                    iconImage("my-icon")));
            });
        }
    
        @Override
        public void onStart() {
            super.onStart();
            mapControl.onStart();
        }
    
        @Override
        public void onResume() {
            super.onResume();
            mapControl.onResume();
        }
    
        @Override
        public void onPause() {
            super.onPause();
            mapControl.onPause();
        }
    
        @Override
        public void onStop() {
            super.onStop();
            mapControl.onStop();
        }
    
        @Override
        public void onLowMemory() {
            super.onLowMemory();
            mapControl.onLowMemory();
        }
    
        @Override
        protected void onDestroy() {
            super.onDestroy();
            mapControl.onDestroy();
        }
    
        @Override
        protected void onSaveInstanceState(Bundle outState) {
            super.onSaveInstanceState(outState);
            mapControl.onSaveInstanceState(outState);
        }
    }
    ```
    
En este momento, si ejecuta la aplicación debería ver un marcador en el mapa, como se muestra aquí:

<center>

![Anclado de mapa de Android](./media/how-to-add-symbol-to-android-map/android-map-pin.png)</center>


## <a name="next-steps"></a>Pasos siguientes

Para agregar más material a la asignación, consulte:

> [!div class="nextstepaction"]
> [Agregar formas a un mapa de Android](https://docs.microsoft.com/azure/azure-maps/how-to-add-shapes-to-android-map)