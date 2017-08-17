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

# Pre-Java8 Date and Calendar Examples

The following snippet demonstrates -

* toString method contains a Timezone
* Date - Month Starts at zero, and year at 1900
* Calendar - Month still starts at zeron, but the year is now fixed

Note this will generate a deprecated API warning

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

# New Features

1. New package – java.time.*
2. Core Classes – LocalDate, LocalTime, LocalDateTime, ZonedDateTime, Period, Duration, Instant
3. Immutable
4. Factory methods

# LocalDate And LocalTime Examples

The following snippet demonstrates -

* LocalDate - Date without Timezone
* LocalTime - Time without Timezone

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
    LocalDate currentLocalDate = LocalDate.now();
    System.out.println("currentLocalDate - yyyy-MM-dd - " + currentLocalDate);

    // Month now not based on 0, and year not based on 1900
    LocalDate twentySevenFeb2017LocalDate = LocalDate.of(2017, 2, 27);
    System.out.println("twentySevenFeb2017LocalDate - yyyy-MM-dd - " + twentySevenFeb2017LocalDate);

    twentySevenFeb2017LocalDate = twentySevenFeb2017LocalDate.withYear(2017).withMonth(12).withDayOfMonth(25);
    System.out.println("twentySevenFeb2017LocalDate - with -  " + twentySevenFeb2017LocalDate);

    LocalDate parseTwentySevenFeb2017LocalDate = LocalDate.parse("2017-02-27", DateTimeFormatter.ofPattern("yyyy-MM-dd"));
    System.out.println("parseTwentySevenFeb2017LocalDate - pattern - yyyy-MM-dd - " + parseTwentySevenFeb2017LocalDate);
    
    // increment using plus, decrement using minus
    twentySevenFeb2017LocalDate = twentySevenFeb2017LocalDate.plusDays(1);
    System.out.println("twentySevenFeb2017LocalDate - immutable - " + twentySevenFeb2017LocalDate);
    
    // Time with no date
    LocalTime currentLocalTime = LocalTime.now();
    System.out.println("currentLocalTime - yyyy-MM-dd - " + currentLocalTime);
    
    LocalTime parseLocalTime = LocalTime.parse("13:44");
    System.out.println("parseLocalTime - " + parseLocalTime);

    parseLocalTime = LocalTime.parse("13:44:25");
    System.out.println("parseLocalTime - immutable - " + parseLocalTime);
//{ autofold
}

}
//}
```

# LocalDateTime Examples

* Combines LocalDate and LocalTime
* Called through factory methods of, now, parse
* Immutable
* No TimeZone

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
		LocalDateTime currentLocalDateTime = LocalDateTime.now();
		System.out.println("currentLocalDateTime " + currentLocalDateTime);		

		currentLocalDateTime = LocalDateTime.parse("2019-06-21T23:53:00.123");
		System.out.println("currentLocalDateTime - parse -  " + currentLocalDateTime);

		currentLocalDateTime = currentLocalDateTime.minusYears(10);
		System.out.println("currentLocalDateTime - minus 10 years -  " + currentLocalDateTime);
//{ autofold
}

}
//}
```

# ZonedDateTime

* Associate DateTime with TimeZone

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
		ZonedDateTime zonedDateTime = ZonedDateTime.of(LocalDateTime.now(), ZoneId.systemDefault());
		System.out.println("zonedDateTime - " + zonedDateTime);

		ZoneId australiaSydneyZoneId = ZoneId.of("Australia/Sydney");
		ZonedDateTime australiaSydneyZonedDateTime = ZonedDateTime.of(LocalDateTime.now(), australiaSydneyZoneId);
		System.out.println("australiaSydneyZonedDateTime - " + australiaSydneyZonedDateTime);
//{ autofold
}

}
//}
```

# CustomAdjuster

* The adjuster will adjust a date according to the defined rule

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
    TemporalAdjuster dueDateAdjuster = TemporalAdjusters.ofDateAdjuster((LocalDate localDate) -> localDate.plusWeeks(40));

    LocalDate startLocalDate = LocalDate.now();
    System.out.println("Due Date - " + startLocalDate.with(dueDateAdjuster));
//{ autofold
}

}
//}
```

# Period Or Duration

* Period - Duration in day, weeks, month, years
* Duration - days, hours, minutes, seconds


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
    // Period - Duration in day, weeks, month, years 
    Period examplePeriod = Period.of(72,6,10);
    System.out.println("examplePeriod " + examplePeriod);

    LocalDate localDatePlusExamplePeriod = LocalDate.now().plus(examplePeriod);
    System.out.println("localDatePlusExamplePeriod " + localDatePlusExamplePeriod);
    
    // Duration - days, hours, minutes, seconds
    Duration exampleDuration = Duration.ofHours(5);
    System.out.println("exampleDuration " + exampleDuration);
    
    LocalTime exampleDurationLocalTime = LocalTime.now().plus(exampleDuration);
    System.out.println("exampleDurationLocalTime " + exampleDurationLocalTime);	
//{ autofold
}

}
//}
```

If you have liked this post, check out my personal blog which contains similar tutorials at [www.javabullets.com](https://www.javabullets.com)
