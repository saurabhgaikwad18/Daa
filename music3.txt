import java.util.*;

public class FloydWarshall {
    public static void main(String args[]){
        Scanner sc = new Scanner(System.in);
        final int INF = (int) 1e9;

        System.out.print("Enter No. of Vertex: ");
        int V = sc.nextInt();

        int [][] matrix = new int [V + 1] [ V + 1];

        //intializing the matrix
        for(int i = 1; i <= V; i++){
            for(int j = 1; j <= V; j++ ){
                if (i == j) {
                    matrix[i][j] = 0;
                }
                else{
                    matrix[i][j] = INF;
                }
            }
            
        }

        System.out.print("Enter No. of Edges: ");
        int E = sc.nextInt();


        System.out.println("Enter the Edges(source, destination, weight)'u v w'");

        for(int i = 0 ;  i < E ; i++){
            int u = sc.nextInt();
            int v = sc.nextInt();
            int w = sc.nextInt();

            matrix[u][v] = w;
        }

        //floyWarshall algorithm
        for(int k = 1; k <= V ; k++){
            for(int i = 1; i <= V ; i++){
                for(int j = 1; j <= V ; j++){
                    if (matrix[i][k] != INF && matrix[k][j] != INF) {
                        matrix[i][j] = Math.min(matrix[i][j], matrix[i][k] + matrix[k][j]);
                    }
                }
            }

        }

        for(int i = 1; i <= V; i++){
            for(int j = 1; j <= V; j++){
                if (matrix[i][j] == INF) {
                    System.out.print( "-1 ");
                }
                else{
                    System.out.print(matrix[i][j] + "   ");
                }
            }
            System.out.println();
        }
        sc.close();
    }
}
