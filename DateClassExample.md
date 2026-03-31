# 🧪 Java Date Classes — Combined Examples

```java
// Import all required packages
import java.util.Date;
import java.util.Calendar;
import java.time.LocalDate;
import java.time.LocalTime;
import java.time.LocalDateTime;
import java.time.format.DateTimeFormatter;
import java.time.Period;

public class Main {
    public static void main(String[] args) {

        // =========================
        // 1. java.util.Date
        // =========================
        Date d = new Date();
        System.out.println("Current Date (Date): " + d);

        // =========================
        // 2. java.util.Calendar
        // =========================
        Calendar cal = Calendar.getInstance();
        System.out.println("Year: " + cal.get(Calendar.YEAR));
        System.out.println("Month (0-based): " + cal.get(Calendar.MONTH));
        System.out.println("Day: " + cal.get(Calendar.DATE));

        // =========================
        // 3. LocalDate
        // =========================
        LocalDate today = LocalDate.now();
        System.out.println("Today: " + today);
        System.out.println("After 5 days: " + today.plusDays(5));
        System.out.println("Year: " + today.getYear());

        // =========================
        // 4. LocalTime
        // =========================
        LocalTime time = LocalTime.now();
        System.out.println("Current Time: " + time);
        System.out.println("After 2 hours: " + time.plusHours(2));

        // =========================
        // 5. LocalDateTime
        // =========================
        LocalDateTime now = LocalDateTime.now();
        System.out.println("Current DateTime: " + now);
        System.out.println("2 hours ago: " + now.minusHours(2));

        // =========================
        // 6. DateTimeFormatter
        // =========================
        DateTimeFormatter formatter =
                DateTimeFormatter.ofPattern("dd-MM-yyyy");
        String formattedDate = today.format(formatter);
        System.out.println("Formatted Date: " + formattedDate);

        // =========================
        // 7. Period (Age Calculation)
        // =========================
        LocalDate birth = LocalDate.of(2000, 5, 10);
        Period p = Period.between(birth, today);
        System.out.println("Age (years): " + p.getYears());
    }
}
```
