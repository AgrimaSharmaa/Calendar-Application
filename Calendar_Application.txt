import java.util.Scanner;

public class CalendarApplication {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        
        System.out.println("=== Welcome to Java Calendar Application ===");
        System.out.print("Enter Year: ");
        int year = scanner.nextInt();
        
        System.out.print("Enter Month (1-12): ");
        int month = scanner.nextInt();
        
        if (month < 1 || month > 12) {
            System.out.println("Invalid Month! Please run again.");
            return;
        }
        
        printMonthCalendar(year, month);
        scanner.close();
    }
    
    public static void printMonthCalendar(int year, int month) {
        String[] months = {
            "", "January", "February", "March", "April", "May", "June",
            "July", "August", "September", "October", "November", "December"
        };
        
        int[] days = { 0, 31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31 };
        
        // Check for leap year
        if (month == 2 && isLeapYear(year)) {
            days[2] = 29;
        }
        
        System.out.println("\n    " + months[month] + " " + year);
        System.out.println("Su Mo Tu We Th Fr Sa");
        
        int d = getStartDay(year, month);
        
        for (int i = 0; i < d; i++) {
            System.out.print("   ");
        }
        for (int i = 1; i <= days[month]; i++) {
            System.out.printf("%2d ", i);
            if (((i + d) % 7 == 0) || (i == days[month])) {
                System.out.println();
            }
        }
    }
    
    public static boolean isLeapYear(int year) {
        return (year % 400 == 0) || ((year % 100 != 0) && (year % 4 == 0));
    }
    
    public static int getStartDay(int year, int month) {
        // Zeller's Congruence algorithm to find day of week
        if (month == 1 || month == 2) {
            month += 12;
            year--;
        }
        int q = 1; // 1st day of month
        int m = month;
        int k = year % 100;
        int j = year / 100;
        int h = (q + 13 * (m + 1) / 5 + k + k / 4 + j / 4 + 5 * j) % 7;
        
        // Convert to Sunday-based index (0=Sun, 1=Mon, ..., 6=Sat)
        return (h + 5) % 7; 
    }
}
