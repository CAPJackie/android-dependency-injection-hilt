
En este parte tienes que implementar la configuración para poder utilizar [inyección de dependencias con Hilt](https://developer.android.com/training/dependency-injection/hilt-android) en tu Task Planner App. El laboratorio muestra el código ejemplo para implementar el modelo de inyección de dependencias utilizando un ejemplo ( GoogleAnalyticsService ). La idea es que apliques el mismo concepto para tu configuración de Retrofit y en base al anterior laboratorio

1.  Agrega la dependencia y plugin necesarios para hacer funcionar Hilt:
2. Añade en el build.gradle a nivel de proyecto el siguiente plugin:

	```groovy
	buildscript {
		...
		ext.hilt_version = '2.40'
		dependencies {
		    ...
		    classpath "com.google.dagger:hilt-android-gradle-plugin:$hilt_version"    
	    }
	}
	```
    
3.  agrega en el build.gradle del app el plugin que acabaste de instalar

	```groovy
	plugins { 
	   ...
	   id 'dagger.hilt.android.plugin'
	}
	android {
	   ...
	}
	```

4. Añade la dependencia de hilt a tu app build.gradle de la siguiente manera:
   ```groovy
	implementation "com.google.dagger:hilt-android:$hilt_version"
	annotationProcessor 'com.google.dagger:hilt-compiler:$hilt_version'
	```
	
6.  Crea una clase que extienda a **Application** ( de android.app.Application ), agrega la anotación de Hilt:
    

	```java
	@HiltAndroidApp
	class ExampleApplication extends Application() { ... }
	```


1.  Define la clase [módulo](https://developer.android.com/training/dependency-injection/dagger-android#dagger-modules) de inyección:
    ```java
    @Module
    @InstallIn(SingletonComponent.class)
    class AnalyticsModule {
	    @Provides 
	    public AnalyticsService provideAnalyticsService() { 
		    return GoogleAnalyticsService() 
		}
	}
    ```

1.  Anota alguna de tus actividades con @AndroidEntryPoint e inyecta tu modulo para verificar que funciona:
    ```java
	@Inject
	AnalyticsService analyticsService;
    ```    


Envía el link de tu repositorio público con tu solución:
