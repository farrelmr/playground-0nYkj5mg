# Java8 – Date and Time examples

This post originally appeared in my blog, [www.javabullets.com](https://www.javabullets.com/java8-date-and-time-examples/) as part of a series covering Java8 features.

We had two date implementations before Java8 – java.util.Date and java.util.Calendar. There were numerous issues with these implementations which Java8 seeks to resolve with its new java.time API.

# Issues

* API Design – java.util.Date and java.util.Calendar both had issues including -
  * months starting from 0
  * in the case of Date year starting from 1900
  * Date also represented a point in time, seconds from the epoch, while its toString method included a TimeZone
  * No single class representing Time or Date
* DateFormat not thread safe

Joda-Time evolved as a defacto standard for Java dates, and its lead developer Stephen Colebourne defined the Java8 JSR-310 API.

# New Features

1. New package – java.time.*
2. Core Classes – LocalDate, LocalTime, LocalDateTime, ZonedDateTime, Period, Duration, Instant
3. Immutable
4. Factory methods

# Examples

You can create a runnable code snippet using the `runnable` keyword:

```java runnable
// { autofold
import java.text.DateFormat;
import java.text.SimpleDateFormat;
import java.time.Duration;
import java.time.LocalDate;
import java.time.LocalDateTime;
import java.time.LocalTime;
import java.time.Period;
import java.time.ZoneId;
import java.time.ZonedDateTime;
import java.time.format.DateTimeFormatter;
import java.time.temporal.TemporalAdjuster;
import java.time.temporal.TemporalAdjusters;
import java.util.Calendar;
import java.util.Date;
import java.util.GregorianCalendar;

public class Main {

public static void main(String[] args) {

// }

		System.out.println("\npreJava8DateAndCalendar\n");

		Date today = new Date();
		System.out.println("Note the time includes the default timezone - " + today.toString());

		Date twentySevenFeb2017Date = new Date(117, 1, 27);
		System.out.println("Now deprecated new Date(day, month, year) - but note month starts at zero, and year 1900 - " + twentySevenFeb2017Date);

		Calendar twentySevenFeb2017Calendar = new GregorianCalendar(2017,1,27);
		System.out.println("Calendar - month starts at zero, and but year fixed - " + twentySevenFeb2017Calendar.getTime());

		DateFormat ddMMyyySDF = new SimpleDateFormat("dd/MM/yyyy");
		System.out.println("DateFormat not ThreadSafe - " + ddMMyyySDF.format(twentySevenFeb2017Date));
//{ autofold
}

}
//}
```

# Advanced usage

For more complex playgrounds, you can use this [Java template](https://github.com/TechDotIO/java-template)
