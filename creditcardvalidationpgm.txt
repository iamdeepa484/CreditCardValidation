import java.util.Scanner;

public class Main {

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.print("Enter the credit card number: ");
        long cnumber = scanner.nextLong();
        System.out.println(cnumber + " is " + (validitychk(cnumber) ? "valid" : "invalid"));
        scanner.close();
    }

    public static boolean validitychk(long cnumber) {
        return (thesize(cnumber) >= 13 && thesize(cnumber) <= 16) &&
                (prefixmatch(cnumber, 4) || prefixmatch(cnumber, 5) || prefixmatch(cnumber, 37) || prefixmatch(cnumber, 6)) &&
                ((sumdoubleeven(cnumber) + sumodd(cnumber)) % 10 == 0);
    }

    public static int sumdoubleeven(long cnumber) {
        int sum = 0;
        String num = Long.toString(cnumber);
        for (int i = thesize(cnumber) - 2; i >= 0; i -= 2)
            sum += getDigit(Character.getNumericValue(num.charAt(i)) * 2);
        return sum;
    }

    public static int getDigit(int cnumber) {
        if (cnumber < 9)
            return cnumber;
        return cnumber / 10 + cnumber % 10;
    }

    public static int sumodd(long cnumber) {
        int sum = 0;
        String num = Long.toString(cnumber);
        for (int i = thesize(cnumber) - 1; i >= 0; i -= 2)
            sum += Character.getNumericValue(num.charAt(i));
        return sum;
    }

    public static boolean prefixmatch(long cnumber, int d) {
        return getprefx(cnumber, thesize(d)) == d;
    }

    public static int thesize(long d) {
        return Long.toString(d).length();
    }

    public static long getprefx(long cnumber, int k) {
        String num = Long.toString(cnumber);
        if (num.length() > k) {
            return Long.parseLong(num.substring(0, k));
        }
        return cnumber;
    }
}
