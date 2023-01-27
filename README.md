# TicTacToe



import java.util.Scanner;

public class TicTacToe {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        char[][] game = new char[3][3];
        boolean isX = false;
        boolean isO = false;
        boolean isDraw = false;
        boolean isEven = false;

        printGame(game);

        while (!isX && !isO && !isDraw) {
            String input = scanner.nextLine();

            if (!input.matches("^\\s*\\d\\s+\\d\\s*$")) {
                System.out.println("You should enter numbers!");
            } else {
                String[] arrOfStr = input.split(" ");

                int coordinateUser1 = Integer.parseInt(arrOfStr[0]);
                int coordinateUser2 = Integer.parseInt(arrOfStr[1]);

                boolean isMovable = true;

                if (coordinateUser1 > 3 || coordinateUser2 > 3) {
                    isMovable = false;
                    System.out.println("Coordinates should be from 1 to 3!");
                } else if (game[coordinateUser1 - 1][coordinateUser2 - 1] != 0) {
                    isMovable = false;
                    System.out.println("This cell is occupied! Choose another one!");
                }

                if (isMovable) {
                    if (!isEven) {
                        game[coordinateUser1 - 1][coordinateUser2 - 1] = 'X';
                        isEven = true;
                    } else {
                        game[coordinateUser1 - 1][coordinateUser2 - 1] = 'O';
                        isEven = false;
                    }

                    printGame(game);

                    if (isWinner('X', game)) {
                        isX = true;
                        System.out.println("X wins");
                    } else if (isWinner('O', game)) {
                        isO = true;
                        System.out.println("O wins");
                    } else if (isDraw(game)) {
                        isDraw = true;
                        System.out.println("Draw");
                    }
                }
            }
        }
    }

    public static boolean isWinner(char player, char[][] game) {
        return isHorizontalWin(player, game) ||
                isVerticalWin(player, game) ||
                isDiagonalWin(player, game);
    }

    public static boolean isHorizontalWin(char player, char[][] game) {
        return game[0][0] + game[0][1] + game[0][2] == player * 3 ||
                game[1][0] + game[1][1] + game[1][2] == player * 3 ||
                game[2][0] + game[2][1] + game[2][2] == player * 3;
    }

    public static boolean isVerticalWin(char player, char[][] game) {
        return game[0][0] + game[1][0] + game[2][0] == player * 3 ||
                game[0][1] + game[1][1] + game[2][1] == player * 3 ||
                game[0][2] + game[1][2] + game[2][2] == player * 3;
    }

    public static boolean isDiagonalWin(char player, char[][] game) {
        return game[0][0] + game[1][1] + game[2][2] == player * 3 ||
                game[2][0] + game[1][1] + game[0][2] == player * 3;
    }

    public static boolean isDraw(char[][] game) {
        for (int i = 0; i < 3; i++) {
            for (int j = 0; j < 3; j++) {
                if (game[i][j] == 0) {
                    return false;
                }
            }
        }

        return true;
    }

    public static void printGame(char[][] game) {
        System.out.println("---------");
        for (int i = 0; i < 3; i++) {
            System.out.print("| ");
            for (int j = 0; j < 3; j++) {
                if (game[i][j] == 0) {
                    System.out.print("  ");
                } else {
                    System.out.print(game[i][j] + " ");
                }
            }
            System.out.println("|");
        }
        System.out.println("---------");
    }
}
