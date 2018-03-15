# TryOuts
import java.io.*;
import java.util.*;
import java.text.*;
import java.math.*;
import java.util.regex.*;

public class Solution {
   
    static String gridSearch(String[] G, String[] P) {
        // Complete this function
        String output="NO";
    	int ptr=0;
    	boolean flag,ext=false;
    	List<Integer> tmp = new ArrayList<Integer>(); 
    	List<List<Integer>> lastStoneList = new ArrayList<List<Integer>>();
    	List<Integer> ptrList = new ArrayList<Integer>();
    	List<Integer> rowList = new ArrayList<Integer>();
    	
    	for(int i=0;i<P.length;i++){
    		flag=false;
    		ptr=0;
    		for(int j=0;j<G.length;j++){
    			while((G[j].indexOf(P[i],ptr))!=-1 && !(rowList.contains(j))){
    				ptr=G[j].indexOf(P[i],ptr)+1;
    				ptrList.add(ptr-1);
    				flag=true;
    			}
    			if(flag){
    				rowList.add(j);
    				break;
    			}	
    			
    		}
    		
    		if(ptrList.size()>0){    			
    			lastStoneList.add(new ArrayList(ptrList));
    			while(ptrList.size()>0){
    				ptrList.remove(0);
    			}    				   			
    		}else{
    			output="NO";
    			ext=true;
    			break;
    		}
    		
    	}
    	
    	
    	if(rowList.size()==P.length){
	    	if(lastStoneList.size()>0 && !ext){
	    		tmp=lastStoneList.get(0);
	    		Iterator itr = tmp.iterator();
	    		int val,count;
	    		while(itr.hasNext()){
	    			val=(int)itr.next();
	    			count=0;
	    			for(int j=1;j<lastStoneList.size();j++){
	    				if(lastStoneList.get(j).contains(val)){
	    					count+=1;
	    					continue;
	    				}
	    					
	    			}
	    			if(count==lastStoneList.size()-1){
	    				output="YES";
	    				break;
	    			}    			
	    		}
	    		
	    	}
	    	
    	}
    
    	return output;
    }

    public static void main(String[] args) {
        Scanner in = new Scanner(System.in);
        int t = in.nextInt();
        for(int a0 = 0; a0 < t; a0++){
            int R = in.nextInt();
            int C = in.nextInt();
            String[] G = new String[R];
            for(int G_i = 0; G_i < R; G_i++){
                G[G_i] = in.next();
            }
            int r = in.nextInt();
            int c = in.nextInt();
            String[] P = new String[r];
            for(int P_i = 0; P_i < r; P_i++){
                P[P_i] = in.next();
            }
            String result = gridSearch(G, P);
            System.out.println(result);
        }
        in.close();
    }
}

