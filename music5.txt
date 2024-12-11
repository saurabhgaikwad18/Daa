import java.util.*;;

public class KnightTour {

    static int N;

    static boolean isSafe(int x, int y, int[][] solution){
        if (x >= 0 && x < N && y >= 0 && y < N && solution[x][y] == -1) {
            return true;
        }
        return false;
    }

    static void print(int[][] sol) {
        for (int i = 0; i < N; i++) {
            for (int j = 0; j < N; j++) {
                System.out.print(sol[i][j] + " ");
            }
            System.out.println();
        }
    }

    static boolean solveKt(int x, int y){
        int[][] solution = new int[N][N];

        for (int i = 0; i < N; i++) {
            for (int j = 0; j < N; j++) {
                solution[i][j] = -1;
            }
        }


        int xMove [] = {2, 1 ,-1 ,-2 , -2, -1, 1, 2};
        int yMove [] = {1, 2, 2, 1, -1, -2, -2, -1};

         // Mark the starting position as the first move
         solution[x][y] = 0;

        int movei = 1; 

        if (!solvekTuntil(x, y, solution, movei, xMove, yMove)) {
            System.out.println("No solution exists for the given board size and starting point.");
            return false;
        }
        else{
            print(solution);
        }
        return true;
    }

    static boolean solvekTuntil(int x, int y,int[][] solution,  int movei, int[]xMove, int[]yMove){

        if (movei == N*N) {
            return true;
        }

        for(int i = 0; i < 8; i++){
            int next_x = x + xMove[i];
            int next_y = y + yMove[i];

            if (isSafe(next_x, next_y, solution)) {
                solution[next_x][next_y] = movei;
                if (solvekTuntil(next_x, next_y, solution, movei + 1, xMove, yMove)) {
                    return true;
                }
                else{
                    solution[next_x][next_y] = -1;
                }

            }  
        }
        return false;
    }
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        System.out.print("Enter the size of chessBoard: ");
        N = sc.nextInt();

        System.out.print("Enter the starting point(x,y): ");
        int x = sc.nextInt();
        int y = sc.nextInt();


        solveKt(x,y);

        sc.close();
    }
    
}