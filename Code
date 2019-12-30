/* Author: Kevin Xu, Edwin Tian
 * Date: March. 24. 2019
 */

import java.util.Scanner;
import java.util.ArrayList;
import java.util.*;

public class breaker {
    static Scanner in = new Scanner(System.in);
    static final String VALID_CHARS = "BGOYRP";
    static final int SIZE = 4;
    static final int TRIES = 10;             

    public static void main(String[] args){
        char[] secretCode = new char[SIZE];
        String userInput = "";
        char[][] guesses = new char[TRIES][SIZE];
        char[][] clues = new char[TRIES][SIZE];
        ArrayList <Character> gResult = new ArrayList<>();
        int numTry = 0;
        boolean win = true;
        System.out.println("Welcome to codebreakers!");
        
        //create secret code
        secretCode = createCode(VALID_CHARS, SIZE);        
        //printArray(secretCode);
        do {
                //get user input and validate
                System.out.println("\nPlease enter your guess of length " + SIZE + " using the letters '" + VALID_CHARS +"'");        
                userInput = in.next().toUpperCase();
                char[] charInput = userInput.toCharArray();

                //validate 
                while(valid(charInput, VALID_CHARS, SIZE) == false) {
                    System.out.println("Please enter your guess again of length " + SIZE + " using the letters '" + VALID_CHARS + "' ");
                    userInput = in.next().toUpperCase();
                    charInput = userInput.toCharArray();
                }
                //save users' guess to 2D array
                for(int i = 0; i < charInput.length;i++) {
                        guesses[numTry][i] = charInput[i];
                }
                //get user's guess result and save to 2D array
                gResult= getGuessResult(secretCode,charInput);
                for(int i = 0; i < gResult.size();i++) {
                        clues[numTry][i] = gResult.get(i);
                }
                win = checkWin(gResult);
                //display the game
                displayGame(numTry, guesses, clues);
                numTry++;
        }while(numTry < TRIES && win == false);

        if(numTry == TRIES && win == false) { 
                System.out.println("I'm sorry you lose. The correct code was " + Arrays.toString(secretCode));
        }else {
                //System.out.println("Congratulations! It took you " + numTry + " guesses to find code!");
                System.out.println("Congratulations! It took you " + numTry + " guesses to find code:" +Arrays.toString(secretCode) );
        }
        System.out.println("End  of Game");
    }      
 
    public static void printList(ArrayList<Character>  list) {
        /*Debug usage only - Print ArrayList*/
        for(int i = 0; i < list.size(); i++) {
            System.out.print(list.get(i));
        }
    }
 
    public static void printArray(char[] ary) {
        /*Debug usage only - Print Array*/
        for(int i = 0; i < ary.length; i++) {
            System.out.print(ary[i]);
        }
    }
    
    /** 
     * checkWin javadoc
     * Set win to true
     * If there is no 4 "B"s, win is false and game is continued
     * 
     * @param     listToCheck       clues(B and W)
     * @return                      boolean variable win
     */  
    public static boolean checkWin(ArrayList<Character> listToCheck) {
     boolean win = true;
     if(listToCheck.size() != SIZE) {
   win = false;
  }else {
   for(int i = 0; i < listToCheck.size();i++) {
    if(!listToCheck.get(i).equals('B')) {
     win = false;
    }
   }
  }
     return win;
    }
    
    public static ArrayList<Character> getGuessResult(char[] sCode, char[] gCode) {
        ArrayList <Character> fullyCorrect = new ArrayList<>();
        ArrayList <Character> colorCorrect = new ArrayList<>();
        ArrayList <Character> result = new ArrayList<>();
        //find all 'B' codes in correct position with right spot
        fullyCorrect = findFullyCorrect(sCode, gCode);
        //find all 'W' codes
        colorCorrect = findColourCorrect(removeFullyCorrect(sCode, gCode), removeFullyCorrect(gCode,sCode));
        //merge colorResult to result
        for (int i=0;i<fullyCorrect.size();i++) {
            result.add(fullyCorrect.get(i));
        }
        for (int i=0;i<colorCorrect.size();i++) {
            result.add(colorCorrect.get(i));
        }
        //printList(result);
        return result;
    }
    ///Required by documents
    public static char[] createCode(String colour, int size){  
        /**
         * Kevin Xu, created on 3/6, updated on 3/13
         * Generate code for player to guess (array of characters) given characters of all colours and size of the code
         * @param    colour -   characters of all colours
         * @param    size   -   size of the code
         * @return   array of characters (code)  
         */
     char[] code = new char[size];
        int index;
     for(int i = 0; i < size; i++){
       index = (int)(Math.random()*colour.length());
       code[i] = colour.charAt(index);
     }
     return code;
    } 
   
 public static boolean valid(char[] listInput, String validChar, int strSize) {
        /* Edwin Tian   blah blah blah
        */
  boolean validInput = true;
   if(listInput.length != strSize) {
    validInput = false;
   }else {
    for(int i = 0; i < listInput.length;i++) {
     if(validChar.indexOf(listInput[i]) == -1) {
      validInput = false;
      break;
     }
    }
   }
  return validInput;
 }

 /** 
  * findFullyCorrect javadoc
  * Create a new list to store "B"
  * Compare each index of the computer generated code and user input code
  * If they match, then "B" (black) is added to the list which is being returned
  * 
  * @param  char[] sCode, char[] gCode  computer generated and user input code
  * @return                             list containing "B"s
  */
 public static ArrayList<Character> findFullyCorrect(char[] sCode, char[] gCode) {
  ArrayList<Character> list = new ArrayList<>();
   for(int i = 0; i < sCode.length;i++) {
    if(gCode[i] == (sCode[i])) {
     list.add('B');
    }
   }
  return list;
 }
 
 /** 
  * removeFullyCorrect javadoc
  * Create a new list to store the removed list
  * Compare each index of the computer generated code and user input code
  * If they do not match, then user input code is being added to the list
  * 
  * @param  char[] sCode, char[] gCode  computer generated and user input code
  * @return                             list containing code after duplicates being removed
  */  
    public static ArrayList<Character> removeFullyCorrect(char[] sCode, char[] gCode){
        ArrayList<Character> list = new ArrayList<>();
        for(int i = 0; i < gCode.length; i++) {
            if(sCode[i]!= gCode[i]) list.add(gCode[i]);
        }
        return list;        
    }
    
 /** 
  * findColourCorrect javadoc
  * Create a new list to store "W" and a new boolean array and set all of the boolean elements to false
  * Compare the computer generated code and user input code (after removing fully correct)
  * If they match, then "W" (white) is added to the colour correct list and check at the index is being set to false
  * 
  * @param  char[] sCodeRemain, char[] gCodeRemain  computer generated and user input code after removing fully correct
  * @return                                         list containing "W"s
  */         
    public static ArrayList<Character> findColourCorrect(ArrayList<Character> sCodeRemain, ArrayList<Character> gCodeRemain ) {
        ArrayList <Character> list = new ArrayList<>();
        boolean[] checked = new boolean[sCodeRemain.size()];
                
        for(int i = 0; i < sCodeRemain.size();i++) {
            checked[i] = false;
        }
        for(int i = 0; i < gCodeRemain.size();i++) {
            for(int j = 0; j < sCodeRemain.size();j++) {
                if ( checked[j]==false) {
                    if( sCodeRemain.get(j)==gCodeRemain.get(i) ) {
                        list.add('W');
                        checked[j]=true;
                        break;
                    }
                }
            }
        }
     return list;
    }
    
    public static void displayGame(int numTry, char[][] allGuess, char[][] allClue) {
    System.out.println("\n****************");
    System.out.println("Guess\tClue");
    for(int r = 0; r <= numTry; r++) {
    for(int c = 0; c < allGuess[r].length;c++) {
      System.out.print(allGuess[r][c]);
    }
    System.out.print("\t");
    for(int c = 0; c < allClue[r].length;c++) {    
      System.out.print(allClue[r][c]);
    }
    System.out.print("\n");
  }
 }
    

        
}
