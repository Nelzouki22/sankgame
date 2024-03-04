#include <iostream>
#include <cstdlib>
#include <conio.h>
#include <windows.h>
using namespace std;

bool gameOver;
const int width = 20;
const int height = 20;
int x, y, fruitX, fruitY;
int tailX[100], tailY[100], nTail;
enum direction { STOP = 0, LEFT, RIGHT, UP, DOWN } dir;
int score;

void SetColor(int value) {
    SetConsoleTextAttribute(GetStdHandle(STD_OUTPUT_HANDLE), value);
}

void Setup() {
    gameOver = false;
    dir = STOP;
    x = width / 2;
    y = height / 2;
    fruitX = rand() % width;
    fruitY = rand() % height;
    score = 0;
}

void Draw() {
    system("cls");
    for (int i = 0; i < width + 2; i++) {
        SetColor(10); // Green color for borders
        cout << "#";
    }
    cout << endl;

    for (int j = 0; j < height; j++) {
        for (int i = 0; i < width; i++) {
            if (i == 0) {
                SetColor(10); // Green color for borders
                cout << "#";
            }

            if (i == x && j == y) {
                SetColor(14); // Yellow color for snake head
                cout << "O";
            }
            else if (i == fruitX && j == fruitY) {
                SetColor(12); // Red color for fruit
                cout << "F";
            }
            else {
                bool isTail = false;
                for (int k = 0; k < nTail; k++) {
                    if (tailX[k] == i && tailY[k] == j) {
                        SetColor(11); // Cyan color for snake tail
                        cout << "o";
                        isTail = true;
                    }
                }
                if (!isTail) {
                    cout << " ";
                }
            }

            if (i == width - 1) {
                SetColor(10); // Green color for borders
                cout << "#";
            }
        }
        cout << endl;
    }

    for (int i = 0; i < width + 2; i++) {
        SetColor(10); // Green color for borders
        cout << "#";
    }
    cout << endl;
    SetColor(15); // White color for text
    cout << "Score: " << score << endl;
}

void Input() {
    if (_kbhit()) {
        switch (_getch()) {
            case 'a':
                dir = LEFT;
                break;
            case 'd':
                dir = RIGHT;
                break;
            case 'w':
                dir = UP;
                break;
            case 's':
                dir = DOWN;
                break;
            case 'x':
                gameOver = true;
                break;
        }
    }
}

void Logic() {
    for (int i = nTail - 1; i > 0; --i) {
        tailX[i] = tailX[i - 1];
        tailY[i] = tailY[i - 1];
    }
    tailX[0] = x;
    tailY[0] = y;

    switch (dir) {
        case LEFT:
            x--;
            break;
        case RIGHT:
            x++;
            break;
        case UP:
            y--;
            break;
        case DOWN:
            y++;
            break;
    }

    if (x >= width) {
        x = 0;
    }
    else if (x < 0) {
        x = width - 1;
    }
    if (y >= height) {
        y = 0;
    }
    else if (y < 0) {
        y = height - 1;
    }

    if (x == fruitX && y == fruitY) {
        fruitX = rand() % width;
        fruitY = rand() % height;
        nTail++;
        score += 10;
    }
}

int main() {
    Setup();

    while (!gameOver) {
        Draw();
        Input();
        Logic();
        Sleep(10);
    }

    return 0;
}
