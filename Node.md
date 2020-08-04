public class Node {
	public int distance;
    public int[] neighbor;
    public boolean isMarked =false;
    public void mark(){
        isMarked = true;
    }

}