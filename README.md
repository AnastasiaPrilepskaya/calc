# calc
import java.io.IOException;
import java.util.Arrays;
import java.util.HashMap;
import java.util.Map;
import java.util.Scanner;


public class AllOperations {

    static Map<Character, Integer> map = new HashMap<>();

    public static void main(String[] args) throws IOException {

        map.put('I', 1);
        map.put('V', 5);
        map.put('X', 10);

        Scanner scanner = new Scanner(System.in);
        String[] stringMassive = scanner.nextLine().split(" ");
        if (stringMassive.length > 3 || stringMassive.length < 3) {
            throw new IOException("необходимо два операнда.");
        }
        String numberOne = stringMassive[0];
        String numberTwo = stringMassive[2];
        boolean isFirstNumArab = isArab(numberOne);// 123 -> true :: IV -> false
        boolean isSecondNumArab = isArab(numberTwo);
        int arab1 = 1;
        int arab2 = 1;

        String[] romanRightNum = {"I", "II", "III", "IV", "V", "VI", "VII", "VIII", "IX", "X"};
        boolean isRomanRightNum1 = Arrays.asList(romanRightNum).contains(stringMassive[0]);
        boolean isRomanRightNum2 = Arrays.asList(romanRightNum).contains(stringMassive[2]);
        if (!isFirstNumArab && isRomanRightNum1) {
            arab1 = romaToArab(numberOne);
        } else {
            arab1 = Integer.parseInt(numberOne);
        }
        if (!isSecondNumArab && isRomanRightNum2) {
            arab2 = romaToArab(numberTwo);
        } else {
            arab2 = Integer.parseInt(numberTwo);
        }

        if (!isFirstNumArab && isSecondNumArab) {
            throw new IOException("т.к. используются одновременно разные системы счисления.");

        } else if (isFirstNumArab && !isSecondNumArab) {
            throw new IOException("т.к. используются одновременно разные системы счисления.");
        }

        if (arab1 > 0 && arab1 <= 10 & arab2 > 0 && arab2 <= 10) {
            int result = 0;
            String symbol = stringMassive[1];
            switch (symbol) {
                case "-":
                    result = (arab1 - arab2);
                    break;
                case "+":
                    result = (arab1 + arab2);
                    break;
                case "*":
                    result = (arab1 * arab2);
                    break;
                case "/":
                    result = (arab1 / arab2);
                    break;
                default:
                    throw new IOException("т.к. формат математической операции не удовлетворяет заданию" +
                            "( только +, -, /, *).");
            }

            boolean b = arab1 >= arab2;

            if (!isFirstNumArab && !isSecondNumArab && !b && symbol.equals("-")) {
                throw new IOException("т.к. в римской системе нет отрицательных чисел.");
            }
            if (!isFirstNumArab && !isSecondNumArab && b) {
                String resultRoman = convertNumToRoman(result);
                System.out.println(resultRoman);

            } else {
                System.out.println(result);
            }


        } else {
            throw new IOException("т.к. формат математической операции не удовлетворяет заданию.");
        }
    }

    public static int romaToArab(String s) { // надо чтобы не считало числа типа IIIIV
        int result = 0;
        int prev = 0;
        for (int i = s.length() - 1; i >= 0; i--) {
            int curr = map.get(s.charAt(i));
            if (curr < prev) {
                result -= curr; // result = result - curr;
            } else {
                result += curr;
            }
            prev = curr;
        }
        return result;
    }

    public static boolean isArab(String number) {
        boolean isOnlyDigits = true;
        for (int i = 0; i < number.length() && isOnlyDigits; i++) {
            if (!Character.isDigit(number.charAt(i))) {
                isOnlyDigits = false;
            }
        }
        return isOnlyDigits;
    }

    private static String convertNumToRoman(int numArabian) {
        String[] roman = {"O", "I", "II", "III", "IV", "V", "VI", "VII", "VIII", "IX", "X", "XI", "XII", "XIII", "XIV",
                "XV", "XVI", "XVII", "XVIII", "XIX", "XX", "XXI", "XXII", "XXIII", "XXIV", "XXV", "XXVI", "XXVII",
                "XXVIII", "XXIX", "XXX", "XXXI", "XXXII", "XXXIII", "XXXIV", "XXXV", "XXXVI", "XXXVII", "XXXVIII",
                "XXXIX", "XL", "XLI", "XLII", "XLIII", "XLIV", "XLV", "XLVI", "XLVII", "XLVIII", "XLIX", "L", "LI",
                "LII", "LIII", "LIV", "LV", "LVI", "LVII", "LVIII", "LIX", "LX", "LXI", "LXII", "LXIII", "LXIV", "LXV",
                "LXVI", "LXVII", "LXVIII", "LXIX", "LXX", "LXXI", "LXXII", "LXXIII", "LXXIV", "LXXV", "LXXVI", "LXXVII",
                "LXXVIII", "LXXIX", "LXXX", "LXXXI", "LXXXII", "LXXXIII", "LXXXIV", "LXXXV", "LXXXVI", "LXXXVII",
                "LXXXVIII", "LXXXIX", "XC", "XCI", "XCII", "XCIII", "XCIV", "XCV", "XCVI", "XCVII", "XCVIII", "XCIX", "C"
        };
        final String s = roman[numArabian];
        return s;
    }

    public static boolean isOk(int i) {
        if (i <= 0 || i > 10) {
            return false;
        }
        return true;
    }

}
