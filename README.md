# Sudoku-Game
#include <graphics.h>
#include <stdlib.h>
#include <stdio.h>
#include <conio.h>

struct player{
char name[20];
char mob[11];
};
void instruction(void)
{
	clrscr();
	textcolor(7);
	printf("\n\n\t\t THIS IS A SUDO_KU GAME ...");
	printf("\n\n\t\t\t INSTRUCTION :-");
	printf("\n\t\t\t NUM LOCK IS ACTIVE \n \t\t\t [8] for up ");
	printf("\n\t\t\t [2] for down\n\t\t\t [6] for right");
	printf("\n\t\t\t [4] for left\n\t\t\t [0] for exit");
	printf("\n\n\t\t\tPress Enter key to insert value ...");
	printf("\n\n\t\t\tPress 00 to EXIT...");
	getch();
	clrscr();
}

void box(int x1,int y1,int x2,int y2)
{
	setcolor(4);
	rectangle(x1,y1,x2,y2);
}

void mbox(int x1,int y1,int x2,int y2)
{
	rectangle(x1+5,y1+5,x2-5,y2-5);
}

void drowbox(char su[][9])
{
	int i,j,c1=150,r1=100;
	char *ch;
	box(c1-5,r1-4,c1+315,r1+306);

	bar(c1-3,r1-2,c1-2,r1+303); /*  coloumn */
	bar(c1-2,r1-2,c1+313,r1-2); /* row */
	for(i=0;i<9;r1=r1+34,c1=150,i++)
	for(j=0;j<9;c1 +=35,j++)
	{
		*ch=su[i][j];
		box(c1,r1,c1+30,r1+30);
		if((j+1)%3==0 )
			bar(c1+32,r1-2,c1+33,r1+32);    /* coloumn */
		if((i+1)%3==0 )
			bar(c1-3,r1+32,c1+32,r1+32);  /* row */
		setcolor(15);
		outtextxy(c1+12,r1+12,ch);
	}
}

void movescreen(char su[][9])
{
	int i=0,j=0,c1=150,r1=100,c2,r2;
	char *chh,ch,vch;
	for(c2=c1,r2=r1;ch !='0';c2=c1,r2=r1)
	{
		if (ch==13)
		{
			vch=getch();
			if(vch>48 &&vch<58)
			{
					su[i][j]=vch;
					*chh=su[i][j];
					setcolor(14);
					setfillstyle(0,0);
					bar(c2+2,r2+2,c2+25,r2+25);
					outtextxy(c1+12,r1+12,chh);
			}
		}
		if(ch=='8')
		{
			if(r1>100)
				r1 -=34;i--;
		}
		else if(ch=='2')
		{
			if(r1<350)
				r1+=34;i++;
		}
		if(ch=='6')
		{
			if(c1<400)
				c1+=35;j++;
		}
		else if(ch=='4')
		{
			if(c1>150)
				c1-=35;j--;
		}
		setcolor(0);
		mbox(c2,r2,c2+30,r2+30);
		setcolor(7);
		mbox(c1,r1,c1+30,r1+30);
		ch=getch();
	}
}
void playerWrite(struct player x){
	char str1[50] = "Name-> ";
	char str2[50] = "Mob-> ";
	// Declare the file pointer
	FILE *filePointer ;

	// Get the data to be written in file
	printf("Enter Your Name:- "); scanf("%s",x.name);
	printf("Enter Your MobileNo:- "); scanf("%s",x.mob);
	strcat(str1,x.name);
	strcat(str2,x.mob);

	// Open the existing file GfgTest.c using fopen()
	// in write mode using "w" attribute
	filePointer = fopen("player.txt", "a") ;

	// Check if this filePointer is null
	// which maybe if the file does not exist
	if ( filePointer == NULL )
	{
		printf( "failed to open." ) ;
	}
	else
	{
		// Write the dataToBeWritten into the file
		if ( strlen (x.name) && strlen(x.mob) > 0 )
		{
		// writing in the file using fputs()
		       fputs(str1, filePointer) ;
		       fputs("\n", filePointer) ;
		       fputs(str2, filePointer) ;
		       fputs("\n\n", filePointer) ;
		}

		// Closing the file using fclose()
		fclose(filePointer) ;
	}
	cleardevice();
}
void playerRead(){


	// Declare the file pointer
	FILE *filePointer ;

	// Declare the variable for the data to be read from file
	char dataToBeRead[50];

	// Open the existing file GfgTest.c using fopen()
	// in read mode using "r" attribute
	filePointer = fopen("player.txt", "r") ;

	// Check if this filePointer is null
	// which maybe if the file does not exist
	if ( filePointer == NULL )
	{
		printf( "file failed to open." ) ;
	}
	else
	{
		// Read the dataToBeRead from the file
		// using fgets() method
		while( fgets ( dataToBeRead, 50, filePointer ) != NULL )
		{

			// Print the dataToBeRead
			printf( "%s" , dataToBeRead ) ;
		}

		// Closing the file using fclose()
		fclose(filePointer) ;
	}
}

void main()
{
   int gdriver = DETECT, gmode, errorcode;
   char ch; struct player x;
   char tsu[9][9]={
	{' ',' ',' '  ,' ','7',' '  ,' ','6',' '},
	{'3',' ','9'  ,' ','6',' '  ,' ',' ','8'},
	{' ','6',' '  ,'2d',' ','3'  ,' ',' ',' '},

	{' ','5','6'  ,' ',' ',' '  ,'4',' ','3'},
	{'7',' ',' '  ,' ',' ',' '  ,' ',' ','2'},
	{'8',' ','2'  ,' ',' ',' '  ,'5','1',' '},

	{' ',' ',' '  ,'1',' ','7'  ,' ','5',' '},
	{'1',' ',' '  ,' ','8',' '  ,'7',' ','9'},
	{' ','8',' '  ,' ','2',' '  ,' ',' ',' '},
	};
   clrscr();
	textcolor(7);
	printf("\n\n\t\t THIS IS A SUDOKU GAME ...");
	printf("\n\n\t\t\tPress Y to PLay AND N For Exit...\t "); scanf("%c",&ch);
	getch();
	clrscr();
if(ch=='Y' || ch =='y'){
   instruction();
   initgraph(&gdriver, &gmode, "c://TURBOC3//BGI");
   drowbox(tsu);
   movescreen(tsu);
   cleardevice();
   playerWrite(x);
   playerRead();
   getch();
   }
   else{
   exit(0);
   }
}
