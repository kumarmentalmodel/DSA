
#### Number of digits in a number

```java
int digits = (int)(Math.log10(n)) +1;
```

### Basic Programs

```java
package com.kumar;  
  
import java.util.Scanner;  
  
public class TicTacToe {  
    public static void main(String[] args) {  
        char[][] board= new char[3][3];  
        for(int row=0;row<board.length;row++){  
            for(int col=0;col<board[row].length;col++){  
                board[row][col] = ' ';  
            }  
        }  
        char player = 'x';  
        boolean gameover = false;  
        Scanner scanner = new Scanner(System.in);  
  
        while(!gameover){  
            printboard(board);  
            System.out.println("Player" + player + "enter: ");  
            int row = scanner.nextInt();  
            int col = scanner.nextInt();  
  
            if(board[row][col] == ' '){  
                //place the element  
                board[row][col] = player;  
                gameover = haveWon(board, player);  
                if(gameover){  
                    System.out.println("Player -> " + player + " has won!!!!");  
                }  
                else{  
                    player = player == 'x' ? 'o' : 'x';  
                }  
            }else{  
                System.out.println("Invalid move");  
            }  
        }  
        printboard(board);  
    }  
  
    public static boolean haveWon(char[][] board, char player){  
        for(int row=0;row<board.length;row++){  
            if(board[row][0] == player && board[row][1] == player &&
             board[row][2] == player){  
                return true;  
            }  
        }  
        for(int col=0;col<board.length;col++){  
            if(board[0][col] == player && board[1][col] == player &&0
             board[2][col] == player){  
                return true;  
            }  
        }  
        if(board[0][1] == player && board[1][1] == player && board[2][2] == player){  
            return true;  
        }  
        if(board[2][0] == player && board[1][1] == player && board[0][2] == player){  
            return true;  
        }  
        return false;  
    }  
    public static void printboard(char[][] board){  
        for(int row=0;row<board.length;row++){  
            for(int col=0;col<board[row].length;col++){  
                System.out.print(board[row][col] + " | ");  
            }  
            System.out.println();  
        }  
    }  
  
}
```