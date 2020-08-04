import java.util.ArrayList;
import java.util.List;
import java.util.Scanner;

public class test1 {
	static int X = Integer.MAX_VALUE;
    public static void main(String[] args) {
        int[][] matrix = {
                {X,3,X,X,X,5,X,1},
                {3,X,2,5,X,X,X,X},
                {X,2,X,X,6,X,X,X},
                {X,5,X,X,1,4,X,X},
                {X,X,6,1,X,X,X,X},
                {5,X,X,4,X,X,2,X},
                {X,X,X,X,X,2,X,6},
                {1,X,X,X,X,X,6,X}
        };
        int root = 0;
        List<Node> nodes = initNodes(matrix,root);
        for(int i=2;i<nodes.size();i++){
            //find the closest node
            Node nearest = getNearestNode(nodes);
            updateNeighbors(nearest,nodes);
            nearest.mark();
        }
        @SuppressWarnings("resource")
		Scanner sc = new Scanner(System.in);
        int loc = sc.nextInt();
        print(nodes,root,loc);
    }
    

    public static List<Node> initNodes(int[][] matrix,int root){
        List<Node> list =new ArrayList<>();
        for(int i=0;i<matrix.length;i++) {
            Node node = new Node();
            if(i==root){
                node.distance =0;
                node.mark();
            }else {
                node.neighbor = matrix[i];
                node.distance = matrix[i][root];
            }
            list.add(node);
        }
        return list;
    }
    public static Node getNearestNode(List<Node> nodes){
        Node nearest =null;
        int i=0;
        for(;i<nodes.size();i++){
            if(!nodes.get(i).isMarked) {
                nearest = nodes.get(i);
                break;
            }
        }
        for(;i<nodes.size();i++){
            if(nodes.get(i).isMarked) {
                continue;
            }
            if(nodes.get(i).distance<nearest.distance) {
                nearest = nodes.get(i);
            }
        }
        return nearest;
    }
    public static void updateNeighbors(Node nearest,List<Node> nodes){
        int[] neighbors = nearest.neighbor;
        for(int i=0;i<neighbors.length;i++){
            if(!nodes.get(i).isMarked&&neighbors[i]!=X){
                checkAndUpdate(nodes.get(i),nearest.distance+neighbors[i]);
            }
        }
    }
    public static void checkAndUpdate(Node neighbor,int sum){
        neighbor.distance =sum>neighbor.distance?neighbor.distance:sum;
    }
    
    public static void print(List<Node> nodes,int root,int loc){
        System.out.println("the shortest distance is:");
        System.out.println(loc+"<->"+root+"="+nodes.get(loc).distance);
    }
}