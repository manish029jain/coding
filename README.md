# coding
 pset4
 1.	When passed strcmp with two strings it compares both strings.if both strings are equal then return 0.
 2.	If(strcmp(g.level,”debug”)==0)
     Int max=9;
     Else
         Int max=1024;
 3. Argc should be 3 and N should not be integer.
 4. Level and y,x.     
 5.Show_cursor;
 6.We can add additional CASE condition at  174,184 .
	  
	  Program for required feature


	  int main(int argc,char *argv[])
	  {
	   Const char *usage=”usage:Sudoku n00b|l33t [#]\n”;
	    If(argc!=2&&argc!=3)
	    {
	     fprintf(stderr,usage);
	     return 1;
	     }
	     if(strcmp(argv[1],"debug")==0)
	     g.level="debug";
	     else if(strcmp(argv[1],"n00b")==0)
	     g.level="n00b"; 
	     else if(strcmp(argv[1],"l33t")==0)
	     g.level="l33t";
	     else
	     {
	     fprintf(stderr,usage);
	     return 2;
	     } 
	     int max=(strcmp(g.level,"debug")==0)?9:1024;
	     if(argc==3)
	     {
	     char c;
	     if(sscanf(argv[2],"%d%c"&g.number,&c)!=1)
	     {fprintf(stderr,usage);
	     return 3;
	     }
	     if(g.number<1||g.number>max)
	     {
	     fprintf(stderr,"that board # doesnot exist!\n");
	     return  4;
	     }
	     srand(g.number);
	     }
	     else
	     {srand(time(null));
	     g.number=rand()%max+1;
	     }
	     if(!startup())
	     {fprintf(stderr,"error starting up ncurses!\n");
	     return 5;
	     }
	     signal (SIGWINCH,(void(*)(int))handle_signal);
	     if(!restart_game())
	     {shutdown();
	     fprintf(stderr,"could not load board from disk!\n");
	     return 6;
	     }
	     redraw all();

	     //to use left,right,top,bottem keys

	     if(KEY_VALUE==LEFT)
	     {if(g.x!=0)
	       g.x-=1;
	       show_cursor
	       }
	       if(KEY_VALUE==RIGHT)
	       {if(g.x!=g.left)
	         g.x+=1;
		 show_cursor
		 }
		 if(KEY_VALUE==UP)
		 {if(g.y!=0)
		   g.y-=1;
		   show_cursor
		   }
		   if(KEY_VALUE==DOWN)
		   {if(g.y!=g.top)
		     g.y+=1;
		     show_cursor
		     }
		     int ch;
		     do
		     {refresh();
		     ch=getch();
		     ch=toupper(ch);
		     switch(ch)
		     {
		     case 'N':
		     g.number=rand()%max+1;
		     if(!restart_game())
		     {shutdown();
		     fprintf(stderr,"could not load board from disk!\n");
		     return 6;
		     }break;
		     case 'R':
		     g.number=rand()%max+1;
		     if(!restart_game())
		     {shutdown();
		     fprintf(stderr,"could not load board from disk!\n");
		     return 6;
		     }break;
		     case CTRL('l')
		     redraw_all();
		     break;
		     }
		     if(ch!=ERR)
		     log_move(ch);
		     }while(ch!='Q'&&check_number());
		     if(!check_number())
		     {attron(COLOR PAIR(PAIR_BORDER));//after successfully  completion of sudoku to change the color 
		     shutdown();
		     printf("congratulations"); //to show congratulation banner
		     }
		     else
		     shutdown();
		     printf("\033[2j");
		     printf("\033[%d;%h",0,0);
		     printf("\nkthxbai!\n\n");
		     return 0;
		     }

		               //to check if sudoku is completed or not
			       bool check_number(void)
			       {
			       for(int i=0;i<9;i++)
			       for(int j=0;j<9;j++)
			       {
			       if(g.board[i][j]==0)
			       return true;
			       }
			       return false;
			       }


























