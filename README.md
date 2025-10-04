
# NCME

No hard debugging on `ConcurrentModificationException` anymore :p

Only support Java 17.

Only support `java.util.HashMap`, `java.util.ArrayList` operations.

Class files compiled from [OpenJDK](https://github.com/openjdk)

## Usage

Add the following JVM argument:
```
--patch-module java.base=NCME-<version>.jar
```

And when `java.util.ConcurrentModificationException` happens, it will log all operations on the object, e.g.:
```
Exception in thread "main" java.util.ConcurrentModificationException
        at java.base/java.util.HashMap.beforeWrite(HashMap.java:472)
        at java.base/java.util.HashMap.putVal(HashMap.java:716)
        at java.base/java.util.HashMap.put(HashMap.java:701)
        at TestHashMap.main(TestHashMap.java:18)
        Suppressed: java.util.ConcurrentModificationException
                at java.base/java.util.HashMap.beforeRead(HashMap.java:447)
                at java.base/java.util.HashMap.forEach(HashMap.java:1596)
                at TestHashMap.mapForEach(TestHashMap.java:24)
                at java.base/java.lang.Thread.run(Thread.java:840)
```
