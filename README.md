# Задача "Исследование JVM через visualVM"

## Описание
Предлагаем вам изучить использование памяти через VisualVM при загрузке новых классов и создании новых объектов

## Инструкция
Скачайте и установите утилиту [VisualVM](https://visualvm.github.io/download.html).  
Откройте её и обратите внимание на раздел `Applications -> Local`

![visualVM-applications-local](images/visualVM-applications-local.png)

Запульте и запустите проект [отсюда](https://github.com/Arsennikum/jvm-visualvm-experience).  
После запуска сразу же (у вас будет на это 30 сек, см. код) щелкните дважды по появившейся запущенной нашей программе в разделе `Local` (о котором упоминалось выше)  
Перейдите на вкладку `Monitor` и можете наблюдать метрики программы в реальном времени. Присмотритесь к разделам `Heap`, `Metaspace`   
![visualVM-heap-metaspace](images/visualVM-heap-metaspace.png)

Когда программа завершится, изучите вывод консоли и код программы (в код можете не погружаться, главное - метод main). Соотнесите с графиками в разделах `Heap`, `Metaspace` и `Classes`

Числовые значения в main методе можете менять по своему усмотрению в соответсвии с вашим железом и как вы считаете, будет показательно.

Сделайте скриншоты графиков и отметьте на них с помощью простого графического редактора и текста, в какие моменты какие действия программы происходили.  
Для выполнения задания нужно отметить на таймлайне графиков каждую строку, которую вывела в консоль программа и пояснить её своими словами в тексте  
Данные скриншоты и текст отправьте в качестве домашнего задания (их также можно добавить в репозиторий. Для текста можете использовать формат Markdown)

## Результат исследования
#### Сведения из консоли
```
> Task :compileJava
> Task :processResources NO-SOURCE
> Task :classes

> Task :JvmExperience.main()
Please open 'ru.netology.JvmExperience' in VisualVm
18:06:40.408295100: loading io.vertx
18:06:40.843174800: loaded 529 classes
```
В момент начала работы программы подсистема загрузчиков классов ClassLoader выд>деляет память в metaspace для информации о константах,полях, методах и имени класса.
![](images/screenClass.png)![](images/metaspaceVertx.png)![](images/screenHeapNetty.png)

```
18:06:43.851698700: loading io.netty
18:06:44.453103600: loaded 2117 classes
```
![](images/screenClassNetty.png)![](images/screenMetaspaceNetty.png)![](images/screenHeapNetty.png)

```
18:06:47.456572900: loading org.springframework
18:06:47.671412900: loaded 869 classes
```
![](images/screenClassSpring.png)![](images/screenMetaspaceSpring.png)![](images/screenHeapSpring.png>)

```
18:06:50.686040600: now see heap
18:06:50.687061200: creating 5000000 objects
18:06:51.017619200: created
```
![](images/screenHeapFive.png)![](images/screenMetaspaceFive.png)![](images/screenClassFive.png>)

```
18:06:54.027263300: creating 5000000 objects
18:06:54.316110200: created
```
![](images/screenHeapFiveMore.png)![](images/screenMetaspaceFiveMore.png)

```
18:06:57.525387300: creating 5000000 objects
18:06:57.941897100: created

BUILD SUCCESSFUL in 55s
2 actionable tasks: 2 executed
18:07:01: Task execution finished 'JvmExperience.main()'.
```
![](images/screenHeapFiveMoreFinish.png)
Программа завершила работу.