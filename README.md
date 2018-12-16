# C-plusplus
#include <iostream>
#include <Windows.h>
#include <iomanip>
#include <conio.h>

using namespace std;

int i_0, j_0;
void SetConsoleWinSizePosition(int width = 0, int heigth = 0, short x_position = 0, short y_position = 0) // Размер консоли
{
	HWND hWnd = GetForegroundWindow();

	HANDLE wHnd = GetStdHandle(STD_OUTPUT_HANDLE);
	SetWindowPos(hWnd, NULL, x_position, y_position, 0, 0, NULL);
	SMALL_RECT windowSize;
	windowSize.Bottom = heigth;
	windowSize.Left = 0;
	windowSize.Right = width;
	windowSize.Top = 0;
	SetConsoleWindowInfo(wHnd, TRUE, &windowSize);
	COORD bufferSize = { width + 1 , heigth + 1 };
	SetConsoleScreenBufferSize(wHnd, bufferSize);
}

enum {
	clBlack, clNavy, clGreen, clTeal, clBrown,
	clPurple, clOlive, clGray, clSilver, clBlue,  //#include < conio.h >
	clLime, clCyan, clRed, clMagneta, clYellow,
	clWhite
};
void SetConsoleColorTextBackground(unsigned short Tex = clWhite, unsigned short Bg = clWhite)
{
	HANDLE hConsole = GetStdHandle(STD_OUTPUT_HANDLE);
	Bg = Bg << 4 | Tex;
	SetConsoleTextAttribute(hConsole, Bg);
}
void print_bin_array(int arr[][4], int row, int col)
{
	system("cls"); // очистка

	
	for (int i = 0; i < row; i++)
	{	cout << "|";
		for (int j = 0; j < col; j++)
		{
			if (arr[i][j] == 0)

				cout << setw(3) << " ";
			
			else 
			
				cout << setw(3) << arr[i][j];	
		
		}
		cout << "|"<<endl;

	}
	
}


void find_zero(int arr[][4], int row, int col)
{
	for (int i = 0; i < row; i++)
	{
		for (int j = 0; j < col; j++)
		{
			if (arr[i][j] == 0)
			{
				i_0 = i;
				j_0 = j;
				return;
			}
		}
	}
}

bool VVV(int mass[][4], int row, int col)
{
	int arr[4][4]{ 1,2,3,4,5,6,7,8,9,10,11,12,13,14,15 };
	for (int i = 0;i< 4; i++)
	{
		for (int j = 0; j < 4; j++)
		{
			if (arr[i][j] != mass[i][j])
				return false;
		}
	}
	return true;
		 
}
void move_up(int arr[][4], int row, int col)
{
	if (i_0 != 0)
	{
		swap(arr[i_0][j_0], arr[i_0 - 1][j_0]);
	}

	print_bin_array(arr, row, col);
	find_zero(arr, row, col);
}
void move_down(int arr[][4], int row, int col)
{
	if (i_0 != 3)
	{
		swap(arr[i_0][j_0], arr[i_0 + 1][j_0]);
	}

	print_bin_array(arr, row, col);
	find_zero(arr, row, col);
}
void move_left(int arr[][4], int row, int col)
{
	if (j_0 != 0)
	{
		swap(arr[i_0][j_0], arr[i_0][j_0 - 1]);
	}

	print_bin_array(arr, row, col);
	find_zero(arr, row, col);
} 
void move_right(int arr[][4], int row, int col)
{
	if (j_0 != 3)
	{
		swap(arr[i_0][j_0], arr[i_0][j_0 + 1]);
	}

	print_bin_array(arr, row, col);
	find_zero(arr, row, col);
}

int main()
{
	const int row = 4, col = 4;
	int arr[row][col]{ 1,2,3,4,5,6,7,8,9,10,11,12,13,14,0,15 };

	SetConsoleWinSizePosition(15, 5);
	
	SetConsoleColorTextBackground(clYellow, clBlack);
	
	print_bin_array(arr, row, col); 
	
	find_zero(arr, row, col);
	

	enum VKey { up = 72, left = 75, right = 77, down = 80};
	int ch = 0, x = 0, y = 0, dir = 0, _x = 0, _y = 0;
	for (;;)
	{
		ch = _getch();
		if (ch == 27) //выход с игры
			break;
		if (ch == 0xe0) //работа клавиш
		{
			ch = _getch();

			switch (ch)
			{
			case up:
			{
				move_up(arr, 4, 4);
				break;
			}

			case left:
			{
				move_left(arr, 4, 4);
				break;
			}

			case right:
			{
				move_right(arr, 4, 4);
				break;
			}

			case down:
			{
				move_down(arr, 4, 4);
				break;
			}
			}
				//if (arr[14 % 4][14 / 4] == 14 + 1)
					//break;
			void show_field();
		}
		if (VVV(arr, row, col))
		{
			cout << "Well done!";
			break;
		}
		
	}
	getchar();
}
