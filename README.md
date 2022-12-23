# Tic-Tac-Toe

#include<stdlib.h>
#include<stdio.h>
#include<conio.h>
#include<DOS.h>

int user_turn=0,tot_turn=0;
char user_name[2][11];
char game_arr[3][3]={{'1','2','3'},{'4','5','6'},{'7','8','9'}};
char flag_win='n',symbol[2]={'X','O'};

void grid_display();
void init_game();
void user_input();
void check_win();

void grid_display(void)
{
int i,j;

clrscr();

printf("\n");
printf("%10s has %c",user_name[0],symbol[0]);
printf("\t\t\t\t%10s has %c",user_name[1],symbol[1]);
printf("\n\n\n");

for(i=0;i<3;i++)
{
	printf("\t\t\t");
	for(j=0;j<3;j++)
	{
		printf("\t%c",game_arr[i][j]);
	}
	printf("\n\n");
}
}

void user_input()
{
int b,m,n;

printf("\n%s Select your place: ",user_name[user_turn]);
scanf("%d",&b);

fflush(stdin);

m = (b-1)/3;
n = (b-1)%3;

if(game_arr[m][n]=='O'||game_arr[m][n]=='X')
{
	printf("\nInvalid input !!!");
	tot_turn--;

	fflush(stdin);
	getchar();

}

else
{
	game_arr[m][n] = symbol[user_turn];

	grid_display();
	check_win();

	user_turn=(user_turn+1)%2;
}
}

void init_game()
{

char choice;
int k;

fflush(stdin);

printf("\n\n\nUSER1 Please enter your name : ");
scanf("%s",user_name[0]);
printf("\nUSER2 Please enter your name : ");
scanf("%s",user_name[1]);

printf("\nPlease choose your symbol ");
printf("\n(A) %s will have O.",user_name[0]);
printf("\n(B) %s will have O.",user_name[1]);
printf("\n(C) Default symbols.");

printf("\n\nPlease enter your choice (A , B or C): ");
fflush(stdin);
scanf("%c",&choice);

if(choice=='A'||choice=='a')
{
	symbol[0]='O';
	symbol[1]='X';
}
else if(choice=='B'||choice=='b'||choice=='C'||choice=='c')
{
	symbol[0]='X';
	symbol[1]='O';
}

printf("\n %s will use %c.",user_name[0],symbol[0]);
printf("\n %s will use %c.",user_name[1],symbol[1]);

printf("\n\n\nThe players have 3 options :");
printf("\n(A) %s will have first turn.",user_name[0]);
printf("\n(B) %s will have first turn.",user_name[1]);
printf("\n(C) Toss will decide first turn.");

printf("\n\nPlease enter your choice (A , B or C): ");
fflush(stdin);
scanf("%c",&choice);

if(choice=='A'||choice=='a')
{
	user_turn = 0;
	printf("\n %s will have the first turn.",user_name[user_turn]);
}
else if(choice=='B'||choice=='b')
{
	user_turn = 1;
	printf("\n %s will have the first turn.",user_name[user_turn]);
}
else
{
	user_turn=rand()%8;
	user_turn*=3;
	user_turn%=2;
	printf("\n Toss in Progress .");
	for(int m=0;m<8;m++)
	{
		delay(500);
		printf(".");
	}
	printf("\n%s wins the toss",user_name[user_turn]);
}

printf("\n\n Press Enter to Continue");

fflush(stdin);
getchar();
}

void check_win()
{
int i=0,j=0;

if(game_arr[0][0]==symbol[user_turn] && game_arr[1][1]==symbol[user_turn] && game_arr[2][2]==symbol[user_turn])
	flag_win='y';

else if(game_arr[0][2]==symbol[user_turn] && game_arr[1][1]==symbol[user_turn] && game_arr[2][0]==symbol[user_turn])
	flag_win='y';

for(i=0;i<3&&flag_win!='y';i++)
	if(game_arr[i][0]==symbol[user_turn] && game_arr[i][1]==symbol[user_turn] && game_arr[i][2]==symbol[user_turn])
		flag_win='y';

for(j=0;j<3&&flag_win!='y';j++)
	 if(game_arr[0][j]==symbol[user_turn] && game_arr[1][j]==symbol[user_turn] && game_arr[2][j]==symbol[user_turn])
		flag_win='y';

if(flag_win=='y')
	printf("\n%s wins the game !!!",user_name[user_turn]);
}

void main()
{
clrscr();
init_game();

for(tot_turn=0;tot_turn<9&&flag_win!='y';tot_turn++)
{

	grid_display();
	user_input();
	//check_win();
	fflush(stdin);
	if(flag_win=='y')
		getchar();

}

//grid_display();
if(flag_win=='n')
	printf("\n\n\t\tTie!!!");

printf("\n\n\n\t\t\t *****GAME OVER!!!***** ");
fflush(stdin);
getchar();
}

