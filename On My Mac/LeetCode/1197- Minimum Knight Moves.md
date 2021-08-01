# 1197. Minimum Knight Moves

**# 1197. Minimum Knight Moves**
**
**
**https://www.youtube.com/watch?v=DD-_hZwEkXY**** **
**https://www.jiuzhang.com/solutions/knight-shortest-path/**** **
**
**
class Coordinate {
    int x;
    int y;
    
    public Coordinate(int x, int y) {
        this.x = x;
        this.y = y;
    }
}

class Solution {
    public int[] directionX = {1, 1, -1, -1, 2, 2, -2, -2};
    public int[] directionY = {2, -2, 2, -2, 1, -1, 1, -1};
    
    public int minKnightMoves(int x, int y) {
        // the reason we have 605 here is that the constrains for this problem is 
        // |x| + |y| < 300. x can be - 300 ~ + 300. Then we leave the middle one 
        // and we also need to give some buffer like from (0,0) to (1,1). we will
        // go out of boud. Since the given chess board in infinite, it can go negative. 
        // so we leave some buffer.
        boolean[][] visited = new boolean[605][605];
        int steps = 0;
        Queue<Coordinate> queue = new LinkedList<>();
        queue.offer(new Coordinate(0, 0));
        
        while (!queue.isEmpty()) {
            int size = queue.size();
            for (int i = 0; i < size; i++) {
                Coordinate coor = queue.poll();
                if (coor.x == x && coor.y == y) {
                        return steps;
                    }
                for (int j = 0; j < directionX.length; j++) {
                    Coordinate nextPosition = new Coordinate(coor.x + directionX[j], 
                                                            coor.y + directionY[j]);
                    // no inbound check here because the chess board is infinite
                    if (!visited[nextPosition.x + 302][nextPosition.y + 302]) {
                         queue.offer(nextPosition);
                         visited[nextPosition.x + 302][nextPosition.y + 302] = true;
                    }    
                }
            }
            // need to put the step++ here because, each time, we need to check the 8 
            // directions it can reach. If from any of those direction, it can reach 
            //the target, then we are done
            steps++;
        }
        return -1;
**    }**
**}**
**
**
![1197- Minimum Knight Moves](images/1197- Minimum%20Knight%20Moves.png)**
**
