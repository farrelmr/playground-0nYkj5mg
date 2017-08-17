# Java8 – Date and Time examples

This post originally appeared in my blog, [www.javabullets.com](https://www.javabullets.com/java8-date-and-time-examples/) as part of a series covering Java8 features.

Before Java8 we had two date implementations – java.util.Date and java.util.Calendar. These implementations had numerous issues which Java8 seeks to resolve. This post considers these issues, as well as providing a examples using the java.time API.

# Issues

1. API Design – java.util.Date and java.util.Calendar both had issues including -
  * months starting from 0
  * in the case of Date year starting from 1900
  * Date also represented a point in time, seconds from the epoch, while its toString method included a TimeZone
  * No single class representing Time or Date
2. DateFormat not thread safe

De-facto standards – Joda-Time evolved as a defacto standard for Java dates, and it is to Java8’s credit that they developed the Java8 JSR-310 API’s with the main joda-time developer Stephen Colebourne.

# New Features

1. New package – java.time.*
2. Core Classes – LocalDate, LocalTime, LocalDateTime, ZonedDateTime, Period, Duration, Instant
3. Immutable
4. Factory methods

# Examples

You can create a runnable code snippet using the `runnable` keyword:

```java runnable
// { autofold
public class Main {

public static void main(String[] args) {
// }

String message = "Hello World!";
System.out.println(message);

//{ autofold
}

}
//}
```

# Advanced usage

For more complex playgrounds, you can use this [Java template](https://github.com/TechDotIO/java-template)
