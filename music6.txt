import java.util.*;

class Node {
    Node parent;
    int pathCost;
    int cost;
    int studentID;
    int clubID;
    boolean[] assigned;

    public Node(int N) {
        assigned = new boolean[N];
    }
}

public class ClubAssignment {
    static int N; 

    static Node newNode(int studentID, int clubID, boolean[] assigned, Node parent) {
        Node node = new Node(N);
        for (int i = 0; i < N; i++) {
            node.assigned[i] = assigned[i];
        }
        if (clubID != -1) {
            node.assigned[clubID] = true;
        }
        node.parent = parent;
        node.studentID = studentID;
        node.clubID = clubID;
        return node;
    }

    static int calculateCost(int x, int y, int[][] costMatrix, boolean[] assigned) {
        int cost = 0;
        boolean[] available = new boolean[N];
        Arrays.fill(available, true);
        for (int i = x + 1; i < N; i++) {
            int min = Integer.MAX_VALUE, minIndex = -1;
            for (int j = 0; j < N; j++) {
                if (available[j] && !assigned[j] && costMatrix[i][j] < min) {
                    min = costMatrix[i][j];
                    minIndex = j;
                }
            }
            available[minIndex] = false;
            cost += min;
        }
        return cost;
    }

    static void printAssignments(Node min) {
        if (min.parent == null) return;
        printAssignments(min.parent);
        System.out.println("Assigned Student " + (char) (min.studentID + 'A') + " to club " + min.clubID);
    }

    static int findMinCost(int[][] costMatrix) {
        PriorityQueue<Node> pq = new PriorityQueue<>(Comparator.comparingInt(node -> node.cost));
        boolean[] assigned = new boolean[N];
        Node root = newNode(-1, -1, assigned, null);
        root.pathCost = root.cost = 0;
        pq.add(root);
        while (!pq.isEmpty()) {
            Node min = pq.poll();
            int i = min.studentID + 1;
            if (i == N) {
                printAssignments(min);
                return min.cost;
            }
            for (int j = 0; j < N; j++) {
                if (!min.assigned[j]) {
                    Node child = newNode(i, j, min.assigned, min);
                    child.pathCost = min.pathCost + costMatrix[i][j];
                    child.cost = child.pathCost + calculateCost(i, j, costMatrix, child.assigned);
                    pq.add(child);
                }
            }
        }
        return 0;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.println("Enter the size of the cost matrix (N): ");
        N = sc.nextInt();

        int[][] costMatrix = new int[N][N];
        System.out.println("Enter the cost matrix: ");
        for (int i = 0; i < N; i++) {
            for (int j = 0; j < N; j++) {
                costMatrix[i][j] = sc.nextInt();
            }
        }

        System.out.println("\nOptimal Cost is " + findMinCost(costMatrix));
        sc.close();
    }
}
