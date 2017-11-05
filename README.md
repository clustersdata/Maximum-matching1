# Maximum-matching1

Maximum matching1

#include <iostream>
  
#include <string>
  
#include <math.h>

#include <vector>
  
using namespace std;

#define M 3001

bool g[M][M];

int mk[M] ,cx[M],pred[M],open[M],cy[M],nx,ny;

//边少适用O(n^3)

int MaxMatchBFS()

{

    int i , u , v , t , d , e , cur , tail , res(0) ;
    
    memset(mk , 0xff , sizeof(mk)) ; 
    
    memset(cx , 0xff , sizeof(cx)) ;
    
    memset(cy , 0xff , sizeof(cy)) ;
    
    for (i = 0 ; i < nx ; i++){
    
        pred[i] = -1 ;
        
		for (open[cur = tail = 0] = i ; cur <= tail && cx[i] == -1 ; cur++){
    
            for (u = open[cur] , v = 0 ; v < ny && cx[i] == -1 ; v ++) if (g[u][v] && mk[v] != i)
            
            {
            
                mk[v] = i ; open[++tail] = cy[v] ; if (open[tail] >= 0) { pred[open[tail]] = u ; continue ; }
                
                for (d = u , e = v ; d != -1 ; t = cx[d] , cx[d] = e , cy[e] = d , e = t , d = pred[d]) ;
                
            }
            
        }
        
        if (cx[i] != -1) res++ ;
        
    }
    
    return res ;
    
}

int path(int u){

    for (int v = 0 ; v < ny ; v++) 
    
		if (g[u][v] && !mk[v]){
    
			mk[v] = 1 ; 
      
			if (cy[v] == -1 || path(cy[v])) {
      
				cx[u] = v ; 
        
				cy[v] = u ; 
        
				return 1 ; 
        
			}
      
		} return 0 ;
    
}

//少适用O(n^3)

int MaxMatchDFS()

{

    int res(0) ;
    
    memset(cx , 0xff , sizeof(cx)) ; 
    
    memset(cy , 0xff , sizeof(cy)) ;
    
    for (int i = 0 ; i < nx ; i++) 
    
		if (cx[i] == -1){
    
			memset(mk , 0 , sizeof(mk)); 
      
            res += path(i) ;
            
		}
    
		return res ;
    
}

