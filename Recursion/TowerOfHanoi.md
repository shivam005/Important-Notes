# Tower of Hanoi
## Find the steps to be used to move all the disk
```
    public void solve(int n , int from, int to,int aux ){
        if(n==1){
            System.out.println("move disc 1 from "+from+" to "+ to);
            return;
        }
         solve(n-1, from , aux, to);
        System.out.println("move disc "+ n+ " from "+from+" to "+ to);
         solve(n-1, aux, to, from);
    }
```
## Find the number of steps to movw the disk
```
    public long toh(int N, int from, int to, int aux) {
        if (N == 1) {
            System.out.println("move disk " + N + " from rod " + from + " to rod " + to);
            return 1;
        }

        long count = toh(N - 1, from, aux, to);

        System.out.println("move disk " + N + " from rod " + from + " to rod " + to);
        count++;

        count += toh(N - 1, aux, to, from);

        return count;
    }
```
