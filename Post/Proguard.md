|Initials| Name  |    Version |  Don't Need |
|:-----: |:-----------:|:-----------:|:-----------:|
|<A HREF="#A">A</A> |
|<A HREF="#B">B</A> |
||<A HREF="#butterknife">ButterKnife</A> |8.x|
|<A HREF="#C">C</A> |
|<A HREF="#I">I</A> |
|<A HREF="#L">L</A> |
|<A HREF="#P">P</A> |
||<A HREF="#pulltorefresh">pulltorefresh</A> ||
|<A HREF="#R">R</A> |
||Realm |2.x|√|
||<A HREF="#retrofit">Retrofit</A> |2.x|
|<A HREF="#S">S</A> |
||<A HREF="#sweetalert">sweetalert</A> |x|
|<A HREF="#U">U</A> |
||<A HREF="#imageloader">Universal Image Loader</A>||
|<A HREF="#V">V</A> |


### [ButterKnife](#butterknife)
```
# Retain generated class which implement ViewBinder.
-keep public class * implements butterknife.internal.ViewBinder { public <init>(); }

# Prevent obfuscation of types which use ButterKnife annotations since the simple name
# is used to reflectively look up the generated ViewBinder.
-keep class butterknife.*
-keepclasseswithmembernames class * { @butterknife.* <methods>; }
-keepclasseswithmembernames class * { @butterknife.* <fields>; }
```

### [pulltorefresh](#pulltorefresh)
```
-dontwarn com.handmark.pulltorefresh.library.**
-keep class com.handmark.pulltorefresh.library.** { *;}
-dontwarn com.handmark.pulltorefresh.library.extras.**
-keep class com.handmark.pulltorefresh.library.extras.** { *;}
-dontwarn com.handmark.pulltorefresh.library.internal.**
-keep class com.handmark.pulltorefresh.library.internal.** { *;}
```

### [Retrofit](#retrofit)
```
-dontwarn retrofit.**
-keep class retrofit.** { *; }
-keepattributes Signature
-keepattributes Exceptions
```

### [sweetalert](#sweetalert)
```
-keep class cn.pedant.SweetAlert.** { *; }
```

### [UniversalImageLoader](#imageloader)
```
-dontwarn com.nostra13.universalimageloader.**
-keep class com.nostra13.universalimageloader.** { *; }
```


