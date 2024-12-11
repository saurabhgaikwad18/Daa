import java.util.*;

public class assign2 {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter the no of jobs:");
        int n = sc.nextInt();
        int[][] task = new int[n][2];
        int maxDeadline = -1;

        for (int i = 0; i < n; i++) {
            System.out.print("Enter deadline (d" + i + "): ");
            int deadline = sc.nextInt();
            System.out.print("Enter profit (p" + i + "): ");
            int profit = sc.nextInt();
            System.out.println(" ");
            if (deadline > maxDeadline) {
                maxDeadline = deadline;
            }
            task[i][0] = profit;
            task[i][1] = deadline;
        }

        int[] schedule = new int[maxDeadline + 1];
        Arrays.fill(schedule, -1); // Initialize all slots as empty (-1)
        Arrays.sort(task, (a, b) -> Integer.compare(b[0], a[0]));

        for (int i = 0; i < n; i++) {
            int profit = task[i][0];
            int deadline = task[i][1];
            for (int j = deadline; j >= 1; j--) {
                if (schedule[j] == -1) { // Assign job to the first available slot
                    schedule[j] = profit;
                    break;
                }
            }
        }

        int result = 0;
        for (int i = 1; i < maxDeadline + 1; i++) {
            if (schedule[i] == -1) {
                System.out.println("Slot " + i + ": Empty");
            } else {
                System.out.println("Slot " + i + ": " + schedule[i]);
                result += schedule[i];
            }
        }

        System.out.println("The maximum Profit is: " + result);
        sc.close();
    }
}
