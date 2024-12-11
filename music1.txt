import java.util.*;
import java.math.BigInteger;

public class Square {

    static BigInteger karatsuba(BigInteger num1, BigInteger num2){

        // Base case: when the numbers are too small, directly multiply them
        if(num1.compareTo(BigInteger.TEN) < 0 || num2.compareTo(BigInteger.TEN) < 0){
            return num1.multiply(num2);
        }

        int half = num1.toString().length() / 2;
        BigInteger tenPowHalf = BigInteger.TEN.pow(half);

        BigInteger a = num1.divide(tenPowHalf);
        BigInteger b = num1.mod(tenPowHalf);

        BigInteger c = num2.divide(tenPowHalf);
        BigInteger d = num2.mod(tenPowHalf);

        BigInteger z0 = karatsuba(b, d); // lower part
        BigInteger z2 = karatsuba(a, c); // upper part
        BigInteger z1 = karatsuba(a.add(b), c.add(d)).subtract(z2).subtract(z0); // middle part

        BigInteger result = z2.multiply(BigInteger.TEN.pow(2 * half))
                             .add(z1.multiply(BigInteger.TEN.pow(half)))
                             .add(z0);
        return result;
    }

    public static void main(String args[]){
        Scanner sc = new Scanner(System.in);

        System.out.print("Enter a large Number: ");
        BigInteger num = sc.nextBigInteger();
        
        System.out.println("\nThe square of the given number is:\n" + karatsuba(num, num));

        sc.close();
    }
}
