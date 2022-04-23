### Offline Qt 5 software development for Android platform. (Qt/QML and C++!)
(2022)

In Russian  
Здесь приводится пример настройки среды Qt, а также собираемого Qt-проекта так, что при этом не требуется Internet для дальнейшей сборки и разработки. Однако очевидно, что необходимые для этого пакеты первично должны быть получены через Internet и использованы в настройках. Пример дается для : Android 4.4, API Level 19 и гарантирует сборку приложения для подобного устройства в offline (у многих есть старенький аппарат, с которым можно поиграться). Однако в ином случае придется действовать по аналогии, и некоторые шаги следует добавить или переопределить, что учтено в данном документе. К счастью, этих шагов совсем мало.
Также предполагается, что получение из Internet больших объемов данных не представляет для вас проблемы, размеры пакетов не отражены.

Документ состоит из двух разделов:  
1. Что делать на хосте с Internet доступом.  
2. Что делать на хосте, где предполагается разработка.  


#### Хост с Internet доступом

###### Qt 5.12.xx
Скачать:  
https://disk.yandex.com/d/jRFOSfSsiFaawg  

###### Qt Creator 4.13.3
Скачать:  
https://disk.yandex.ru/d/DBZo6RiYm6vUUQ  

###### JDK 8
Скачать:  
https://disk.yandex.com/d/qSCJM3Xh7DLWnQ  

###### Gradle
Требуемая Android-ориентированная система сборки для вышеприведенных (версий) средств разработки - это Gradle 4.6.  
Скачать:  
https://disk.yandex.com/d/_8lEARjWqPQDNQ  

###### Android Gradle Plugin
Система Gradle-4.6 работает с Android Gradle Plugin (3.2.0), все компоненты и данные которого, требующиеся при сборке проекта Qt, были отобраны замысловатым путем.  
Скачать:  
https://disk.yandex.com/d/9AEViv5y5R8-dw  


###### Android SDK, NDK, etc...
Скачать:  
https://disk.yandex.ru/d/PyvQAsYXtZHK4g  
Файл AndroidSDK.tgz распаковать в локальную директорию AndroidSDK.

Связка вышеприведенных версий Qt, Qt Сreator, а также целевая платформа, подразумевают, что на хосте разработки должны быть установлены следующие компоненты:
- Android SDK Build-Tools 28.0.3         
- Android SDK Build-Tools 29.0.2         
- Android SDK Command-line Tools (latest)
- Google USB Driver                      
- NDK (Side by side) 21.1.6352462        
- SDK Patch Applier v4                   
- Android SDK Platform-Tools             
- Android SDK Platform 19                
- Android SDK Tools 2.1                  


>Заметьте, что здесь только одна платформа 'Android SDK Platform 19'. Соответствия между версиями Android и Android API Level можно посмотреть здесь:  
>	https://apilevels.com/  
>Установить требуемую платформу (например, 25) следует так:  
>	&nbsp;&nbsp;&nbsp;&nbsp;cd ...\Sdk\cmdline-tools\latest\bin\  
>	&nbsp;&nbsp;&nbsp;&nbsp;sdkmanager.bat --install "platforms;android-25"  
>Убедиться, что платформа установлена:  
>	&nbsp;&nbsp;&nbsp;&nbsp;sdkmanager.bat --list_installed  
>Удалить отныне ненужную платформу 19 (опционально):  
>	&nbsp;&nbsp;&nbsp;&nbsp;sdkmanager.bat --uninstall "platforms;android-19"  
​    
#### Хост разработки

1. Инсталлировать систему Qt 5.12.xx (qt-opensource-windows-x86-5.12.10.exe) с поддержкой разработки под Android (Android Kits) (android_armv7 etc.). Директория установки по умолчанию: C:\Qt\...  
2. Инсталлировать Qt Creator (qt-creator-opensource-windows-x86-4.13.3.exe) в любую директорию.  
3. Инсталлировать JDK (jdk-8u291-windows-x64.exe) в директорию по умолчанию: C:\Program Files\Java\jdk1.8.0_291.  
4. Перенести распакованную директорию AndroidSDK c хоста с Internet на хост разработки в директорию X:\AndroidSDK, (**где "Х" здесь и далее - целевой том**)  
5. Запустить Qt Creator, открыть вкладку Инструменты/Параметры.../Устройства/Android и заполнить следующие настройки:  
	&nbsp;&nbsp;&nbsp;&nbsp;Размещение JDK: C:\Program Files\Java\jdk1.8.0_291  
	&nbsp;&nbsp;&nbsp;&nbsp;Размещение SDK для Android: X:\AndroidSDK\Sdk  

>После определенной паузы следующие настройки должны быть высвечены автоматически:  
>	&nbsp;&nbsp;&nbsp;&nbsp;Список Android NDK:  [ X:\AndroidSDK\Sdk\ndk\21.1.6352462 ]  
>	&nbsp;&nbsp;&nbsp;&nbsp;Путь к Android SDK существует.  
>	&nbsp;&nbsp;&nbsp;&nbsp;Каталог с Android SDK доступен для записи.  
>	&nbsp;&nbsp;&nbsp;&nbsp;Инструменты SDK установлены.  
>	&nbsp;&nbsp;&nbsp;&nbsp;Инструменты платформы установлены.  
>	&nbsp;&nbsp;&nbsp;&nbsp;Инструменты сборки установлены.  
>	&nbsp;&nbsp;&nbsp;&nbsp;Управление SDK работает (для SDK Tools версий не выше 26.х требуется Java только версии 1.8)  
>	&nbsp;&nbsp;&nbsp;&nbsp;SDK платформы установлен.  
>Если есть значок ошибки на надписи "Установлены все необходимые пакеты для всех установленных профилей Qt", оставьте это в стороне.  
>	&nbsp;&nbsp;&nbsp;&nbsp;Размещение собранного OpenSSL: X:\AndroidSDK\Sdk\android_openssl  
>	&nbsp;&nbsp;&nbsp;&nbsp;Настройки OpenSSL в порядке.  

6. Нажать "Ok" для сохранения изменений.  
7. Открыть вкладку Инструменты/Параметры.../Комплекты и убедиться, что для разработки под Android существует следующее:  
	&nbsp;&nbsp;&nbsp;&nbsp;Комплекты  - Android Qt 5.12.xx (android_armv7) Clang armeabi-v7a  
	&nbsp;&nbsp;&nbsp;&nbsp;Профили Qt - C:\Qt\Qt5.12.xx\5.12.xx\android_armv7\bin\qmake.exe  
	&nbsp;&nbsp;&nbsp;&nbsp;Компиляторы - Android Clang (C++,arm,NDK 21.1.6352462)  
	&nbsp;&nbsp;&nbsp;&nbsp;Отладчики - Android Debugger (armeabi-v7a,NDK 21.1.6352462)  
8. Создать новый проект под комплект Android типа android_armv7 (не эмуляция). Запустить сборку и убедиться, что проект *НЕ* собирается (и это исключительно по причине отсутствия Internet)  
9. Перейдите в директорию сборки проекта (android-build). В файле   
	&nbsp;&nbsp;&nbsp;&nbsp;android-build/gradle/wrapper/gradle-wrapper.properties  
	заменить значение:  
	&nbsp;&nbsp;&nbsp;&nbsp;distributionUrl=gradle-4.6-bin.zip  
10. В директорию   
	&nbsp;&nbsp;&nbsp;&nbsp;android-build/gradle/wrapper/  
	поместить файл:  
	&nbsp;&nbsp;&nbsp;&nbsp;gradle-4.6-bin.zip  
11. Содержимое файла android-build/build.gradle привести к следующему виду:  
`	...    `  
` buildscript {`  
&nbsp;&nbsp;`    repositories {`  
&nbsp;&nbsp;&nbsp;&nbsp;`        maven() {`  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;` url  "file:///X:/gradle_repo"`  
&nbsp;&nbsp;&nbsp;&nbsp;`        }`  
&nbsp;&nbsp;`    }`  
&nbsp;&nbsp;`    dependencies {`  
&nbsp;&nbsp;&nbsp;&nbsp;`classpath 'com.android.tools.build:gradle:3.2.0'`  
&nbsp;&nbsp;`    }`  
`}`  
` repositories {`  
&nbsp;&nbsp;`    maven {`  
&nbsp;&nbsp;&nbsp;&nbsp;` url  "file:///X:/gradle_repo"`  
&nbsp;&nbsp;`    }`  
`}`  
`	... `  
12. Распаковать архив  
	&nbsp;&nbsp;&nbsp;&nbsp;gradle_repo.tgz  
	и его содержимое переместить в новую директорию:  
	&nbsp;&nbsp;&nbsp;&nbsp;X:\gradle_repo  
13. В свойствах системы создать переменную окружения  
	&nbsp;&nbsp;&nbsp;&nbsp;GRADLE_USER_HOME  
	со значением 
	&nbsp;&nbsp;&nbsp;&nbsp;X:\gradle-cache:  
	&nbsp;&nbsp;&nbsp;&nbsp;GRADLE_USER_HOME=X:\gradle-cache  
14. Если вы ранее оставили Android SDK Platform 19, то необходимо в файле  
	&nbsp;&nbsp;&nbsp;&nbsp;Qt5.12.xх\5.12.xх\android_armv7\src\android\templates\AndroidManifest.xml  
	из строчки  
	&nbsp;&nbsp;&nbsp;&nbsp;configChanges="..."  
	убрать флаг  
	&nbsp;&nbsp;&nbsp;density  
	(это ошибка разработчиков)  
	А если изменили на свой вариант - действуйте по аналогии: из вышеуказанного AndroidManifest.xml уберите те настройки, которые не поддерживаются в конкретном API Level, о чем будет намекающее сообщение при сборке.  

**После этих операций (если все сделано правильно!) ваш проект должен успешно собираться, подключите устройство и запустите на нем готовое приложение.**

