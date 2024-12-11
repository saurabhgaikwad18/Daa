import java.util.*;

public class Dijkstra {
    static int V;

    // Find the node with the minimum distance that has not been included in the shortest path tree
    int minDist(int dist[], Boolean boolset[]) {
        int min = Integer.MAX_VALUE, min_value = -1;
        for (int i = 0; i < V; i++) {
            if (!boolset[i] && dist[i] <= min) {
                min = dist[i];
                min_value = i;
            }
        }
        return min_value;
    }
    
    // Print the shortest distances from the source node

    void print(int dist[]) {
        System.out.println("Vertex \t Distance from Source");
        for (int i = 0; i < V; i++) {
            System.out.println(i + " \t " + dist[i]);
        }
    }

    // Dijkstra's Algorithm to find the shortest paths from the source node
    void dijkstra(int[][] graph, int src) {
        int dist[] = new int[V];
        Boolean boolset[] = new Boolean[V];

        //Initialize distances and the boolean set array
        for (int i = 0; i < V; i++) {
            dist[i] = Integer.MAX_VALUE;
            boolset[i] = false;
        }

        dist[src] = 0;

        //Dijkstra's main loop
        for (int i = 0; i < V; i++) {
            int u = minDist(dist, boolset);
            boolset[u] = true;

            for (int v = 0; v < V; v++) {
                if (!boolset[v] && graph[u][v] != 0 && dist[u] != Integer.MAX_VALUE && dist[u] + graph[u][v] < dist[v]) {
                    dist[v] = dist[u] + graph[u][v];
                }
            }
        }

        print(dist);
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        System.out.println("Enter the number of vertices in the graph:");
        V = sc.nextInt(); // Let the user define the size of the graph

        int graph[][] = new int[V][V];

        System.out.println("Enter the adjacency matrix for the graph (use 0 for no edge):");
        for (int i = 0; i < V; i++) {
            for (int j = 0; j < V; j++) {
                graph[i][j] = sc.nextInt();
            }
        }

        Dijkstra t = new Dijkstra();

        System.out.println("Enter the starting node:");
        int startNode = sc.nextInt();

        t.dijkstra(graph, startNode);

    }
}
