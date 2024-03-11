import java.util.Scanner;

public class TicTacToe {
    private static char[][] board = new char[3][3];
    private static char currentPlayer = 'X';

    public static void main(String[] args) {
        initializeBoard();
        displayBoard();

        while (!isGameOver()) {
            makeMove();
            displayBoard();
            switchPlayer();
        }

        char winner = checkWinner();
        if (winner == ' ') {
            System.out.println("It's a draw!");
        } else {
            System.out.println("Player " + winner + " wins!");
        }
    }

    private static void initializeBoard() {
        for (int i = 0; i < 3; i++) {
            for (int j = 0; j < 3; j++) {
                board[i][j] = ' ';
            }
        }
    }

    private static void displayBoard() {
        System.out.println("  0 1 2");
        for (int i = 0; i < 3; i++) {
            System.out.print(i + " ");
            for (int j = 0; j < 3; j++) {
                System.out.print(board[i][j] + " ");
            }
            System.out.println();
        }
    }

    private static void makeMove() {
        Scanner scanner = new Scanner(System.in);
        System.out.println("Player " + currentPlayer + "'s turn:");
        System.out.print("Enter row and column (e.g., 0 0 for top left corner): ");
        int row = scanner.nextInt();
        int col = scanner.nextInt();

        if (isValidMove(row, col)) {
            board[row][col] = currentPlayer;
        } else {
            System.out.println("Invalid move! Try again.");
            makeMove();
        }
    }

    private static boolean isValidMove(int row, int col) {
        return row >= 0 && row < 3 && col >= 0 && col < 3 && board[row][col] == ' ';
    }

    private static void switchPlayer() {
        currentPlayer = (currentPlayer == 'X') ? 'O' : 'X';
    }

    private static boolean isGameOver() {
        return isBoardFull() || checkWinner() != ' ';
    }

    private static boolean isBoardFull() {
        for (int i = 0; i < 3; i++) {
            for (int j = 0; j < 3; j++) {
                if (board[i][j] == ' ') {
                    return false;
                }
            }
        }
        return true;
    }

    private static char checkWinner() {
        // Check rows
        for (int i = 0; i < 3; i++) {
            if (board[i][0] == board[i][1] && board[i][1] == board[i][2] && board[i][0] != ' ') {
                return board[i][0];
            }
        }

        // Check columns
        for (int j = 0; j < 3; j++) {
            if (board[0][j] == board[1][j] && board[1][j] == board[2][j] && board[0][j] != ' ') {
                return board[0][j];
            }
        }

        // Check diagonals
        if ((board[0][0] == board[1][1] && board[1][1] == board[2][2] && board[0][0] != ' ')
                || (board[0][2] == board[1][1] && board[1][1] == board[2][0] && board[0][2] != ' ')) {
            return board[1][1];
        }

        return ' ';
    }
}
