# presentation-1
rock paper scissor
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

// Function to get the name of the move
const char* get_move_name(int move) {
    switch (move) {
        case 0: return "Rock";
        case 1: return "Paper";
        case 2: return "Scissors";
        default: return "Invalid";
    }
}

// Function to determine the winner
// Returns 1 if player1 wins, -1 if player2 wins, 0 if tie
int determine_winner(int p1_move, int p2_move) {
    if (p1_move == p2_move) return 0; // Tie
    if ((p1_move == 0 && p2_move == 2) || // Rock beats Scissors
        (p1_move == 1 && p2_move == 0) || // Paper beats Rock
        (p1_move == 2 && p2_move == 1)) { // Scissors beats Paper
        return 1; // Player 1 wins
    }
    return -1; // Player 2 wins
}

int main() {
    srand(time(NULL)); // Seed random number generator

    printf("Welcome to Rock, Paper, Scissors, Minus One!\n");
    printf("Moves: 0=Rock, 1=Paper, 2=Scissors\n\n");

    while (1) {
        // Player inputs two moves
        int p1_hand1, p1_hand2;
        printf("Enter your two moves (0-2, separated by space): ");
        scanf("%d %d", &p1_hand1, &p1_hand2);
        if (p1_hand1 < 0 || p1_hand1 > 2 || p1_hand2 < 0 || p1_hand2 > 2) {
            printf("Invalid input. Try again.\n");
            continue;
        }

        // Computer generates two random moves
        int p2_hand1 = rand() % 3;
        int p2_hand2 = rand() % 3;

        // Reveal initial moves
        printf("\nInitial Reveal:\n");
        printf("Player: %s and %s\n", get_move_name(p1_hand1), get_move_name(p1_hand2));
        printf("Computer: %s and %s\n", get_move_name(p2_hand1), get_move_name(p2_hand2));

        // Player chooses which hand to keep (1 or 2)
        int p1_keep;
        printf("Which hand do you want to keep? (1 for first, 2 for second): ");
        scanf("%d", &p1_keep);
        if (p1_keep != 1 && p1_keep != 2) {
            printf("Invalid choice. Try again.\n");
            continue;
        }
        int p1_final = (p1_keep == 1) ? p1_hand1 : p1_hand2;

        // Computer randomly chooses which to keep (for simplicity)
        int p2_keep = (rand() % 2) + 1;
        int p2_final = (p2_keep == 1) ? p2_hand1 : p2_hand2;

        printf("Player keeps: %s\n", get_move_name(p1_final));
        printf("Computer keeps: %s\n", get_move_name(p2_final));

        // Determine winner
        int result = determine_winner(p1_final, p2_final);
        if (result == 0) {
            printf("It's a tie! Replay.\n\n");
            continue;
        } else if (result == 1) {
            printf("Player wins!\n");
        } else {
            printf("Computer wins!\n");
        }
        break; // End game after a winner
    }

    return 0;
}
