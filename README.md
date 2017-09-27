# sokuban
#include<stdio.h>
#include<conio.h>
#include<windows.h>
int i,j,k=3,dem=0,win=0,ax=8,ay=8,z=0,p;
char a[10][10],kt,s,s1,s2;
void draw()
{	for(i=0;i<=9;i++)
	{	for(j=0;j<=9;j++)
		{	s=' ';
			if ((i==0)||(i==9)) s=a[i][j];
			if ((j==0)||(j==9)) s=a[i][j];
			for(p=2;p<=k;p++)
				if(i==p&&j==p) s='x';
			if (i==ay&&j==ax) s='A';
			if (i==6&&j==5) s='|';
			if ((i==5&&j==6)||(i==5&&j==7)) s='-';
			if (a[i][j]=='O') s=a[i][j];
			if (a[i][j]=='*') s=a[i][j];
			printf("%c",s);
		}
	printf("\n");
	}	
}
main()
{	for(i=0;i<10;i++)
	{	a[0][i]='*';
		a[i][0]='*';
		a[9][i]='*';
		a[i][9]='*';
	}
	a[2][7]='O';a[6][2]='O';a[2][5]=a[3][5]=a[3][6]=a[4][2]=a[5][5]=a[5][8]=a[7][5]='*';
	do
	{	printf("---GAME DAY THUNG---\n");
		printf("1. PLAY(P)\n2. EXIT(E)\n3. HUONG DAN(H)");
		kt=getch();
		system("cls");
		if (kt=='1'||kt=='p'||kt=='P')
		{	do
			{	system("cls");
				draw();
				printf("\ntimes:%d",dem);
				s1=getch();
				if (s1=='R'||s1=='r') 
					{	start();
					}
				move();
				
				if ((a[2][2]=='O'&&a[3][3]=='O'&&k==3)||(a[2][2])=='O'&&a[3][3]=='O'&&a[4][4]=='O'&&k==4)
				{	system("cls");
					draw();
					printf("---VICTORY---\n1. RESTART(R)\n2. BACK(B)");
					do
					{	s2=getch();
						if (s2=='1'||s2=='R'||s2=='r') 
						{	start();
						}
						else
							if (s2=='2'||s2=='b'||s2=='B') win=1;
					}
					while(s2!='r'&&s2!='R'&&s2!='1'&&s2!='b'&&s2!='B'&&s2!='2');
				}
				if ((ay==5&&ax==6)||(ay==5&&ax==7)||(ay==6&&ax==5))
				{	lose();
				}
				if (a[1][1]=='O'||a[8][8]=='O'||a[1][8]=='O'||a[8][1]=='O')
				{	lose();	
					
				}
				if (dem==50)
				{	a[7][4]='O';
					k++;
				}
				if(dem==100)
				{	lose();
				}
				if (win==1) 
				{	start();
					break;
				}
			}
			while(z==0);
		}
		else 
			if (kt=='2'||kt=='e'||kt=='E') break;
		if (kt=='3'||kt=='h'||kt=='H') 
			{	printf("                     ---HUONG DAN---\n-Di chuyen cac chu O sao cho lai toi cac chu x bang so buoc di ngan nhat\n");
				printf("-Neu qua 50 buoc di chuyen se co them 1 chu O va 1 chu x xuat hien\n");
				printf("-Neu so buoc di chuyen la 100 ban se thua\n");
				printf("-Neu di vao -- ban cung thua\n");
				printf(" BAM 0(orB) de quay lai.");
				do
				{	s2=getch();
					if (s2=='0'||s2=='b'||s2=='B') system("cls");
				}
				while(s2!='0'&&s2!='b'&&s2!='B');
			}
	}
	while (kt!='1'&&kt!='2');
} 
void start()
{	system("cls");
	for(i=1;i<=8;i++)
		for(j=1;j<=8;j++)
			a[i][j]=' ';
	win=0;
	a[2][7]='O';
	ax=ay=8;
	a[6][2]='O';
	dem=0;
	k=3;
	a[2][5]=a[3][5]=a[3][6]=a[4][2]=a[5][5]=a[5][8]=a[7][5]='*';
}
void lose()
{	system("cls");
	draw();
	printf("---DEFEAT---\n1. RESTART(R)\n2. BACK(B)");
	do
	{	s2=getch();
		if (s2=='1'||s2=='r'||s2=='R')
		{	start();
		}	
		else 
			if (s2=='2'||s2=='B'|s2=='b') win=1;
	}
	while(s2!='r'&&s2!='R'&&s2!='1'&&s2!='b'&&s2!='B'&&s2!='2');
}
void move()
{	switch(s1)
			{	case('a'):
				case('A'):
					if (ax>1&&a[ay][ax-1]=='O'&&a[ay][ax-2]=='*') break;
					if (ax>2&&a[ay][ax-1]=='O'&&a[ay][ax-2]=='O') break;
					if (a[ay][ax-1]=='*') break;
					if (ax>1)
					{	if (ax>2&&a[ay][ax-1]=='O')
						{	a[ay][ax-1]=' ';
							a[ay][ax-2]='O';
							ax--;						
						}
						else ax--;
						dem++;
					}
					break;
				case('d'):
				case('D'):
					if (ax<8&&a[ay][ax+1]=='O'&&a[ay][ax+2]=='*') break;
					if (ax<7&&a[ay][ax+1]=='O'&&a[ay][ax+2]=='O') break;
					if (a[ay][ax+1]=='*') break;
					if(ax<8)
					{	if (ax<7&&a[ay][ax+1]=='O')
						{	a[ay][ax+1]=' ';
							a[ay][ax+2]='O';
							ax++;
						}
						else ax++;
						dem++;
					}
					break;
				case('s'):
				case('S'):
					if (ay<8&&a[ay+1][ax]=='O'&&a[ay+2][ax]=='*') break;
					if (ay<7&&a[ay+1][ax]=='O'&&a[ay+2][ax]=='O') break;
					if (a[ay+1][ax]=='*') break;
						if (ay<8)
					{	if (ay<7&&a[ay+1][ax]=='O')
						{	a[ay+1][ax]=' ';
							a[ay+2][ax]='O';
							ay++;
						}
						else ay++;
						dem++;
					}
					break;
				case('w'):
				case('W'):
					if (ay>1&&a[ay-1][ax]=='O'&&a[ay-2][ax]=='*') break;
					if (ay>2&&a[ay-1][ax]=='O'&&a[ay-2][ax]=='O') break;
					if (a[ay-1][ax]=='*') break;
					if (ay>1)
					{	if (ay>2&&a[ay-1][ax]=='O')
						{	a[ay-1][ax]=' ';
							a[ay-2][ax]='O';
						ay--;						
						}
						else ay--;
						dem++;
					}
					break;	
			}
}
