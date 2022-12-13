#include<stdio.h>
#include<conio.h>
int page_str[30],n_pages;
void fifo();
void lru();
void optimal();
void main()
{
 int ch,i;
 char ans;
 //clrscr();
 printf("Total= 20  \n\t\t7 0 1 2 0 3 0 4 2 3 0 3 2 1 2 0 1 7 0 1\n");

   printf("\n\t\tENTER NO PAGES IN REFERENCE STRING::->");
   scanf("%d",&n_pages);

   printf("\n\tENTER %d PAGE NO.S::->",n_pages);

   for(i=0;i<n_pages;i++)
   scanf("%d,",&page_str[i]);

   do
   {
      printf("\n\t\tMENU\n");
      printf("\n\t\t1.FIFO PAGE REPLACEMENT");
      printf("\n\t\t2.LRU PAGE REPLACEMENT");
      printf("\n\t\t3.OPTIMAL");
      printf("\n\t\t4.EXIT");
      printf("\n\t\tENTER YOUR CHOICE::->");
      scanf("%d",&ch);
      switch(ch)
      {
	 case 1:fifo();
	   break;
	 case 2:lru();
	   break;
	 case 3:optimal();
	   break;
      }
      printf("\nDo u want to cont..");
      
      scanf("%c",&ans);
   }while(ans=='y'||ans=='Y');
  getch();
}
void fifo()
{
 int col=0,size_frame,flag,fault=0,page[3]={-1,-1,-1};
 int i=0,j=0,k=0;
  printf("\nENTER SIZE OF PAGE FRAME:");
   scanf("%d",&size_frame);

   printf("\n Page String:\n");

   for(i=0;i<n_pages;i++)
   printf("%d ",page_str[i]);

   printf("\nFIFO PAGE REPLACEMENT ALGO:\n\n");

  for(i=0;i<n_pages;i++)
   {
    for(j=0;j<size_frame;j++)
     {
       flag=1;
       if(page[j]==page_str[i])
	{
	  flag=0;
	  break;
	}
     }
     if(flag==1)
      {
	fault++;
	if(col>=size_frame)
	  col=0;
	page[col++]=page_str[i];
      }
     printf("\n");
    for(k=0;k<size_frame;k++)
     {
       printf("%d",page[k]);
     }
  }
  printf("\nFault:-%d",fault);
}

void lru()
{
   int flag1=0,col=0,i,j,k,min=0,cflag=0,page[3]={-1,-1,-1};
   int cnt[3]={-1,-1,-1,},fault=0,size_frame;

   printf("\nENTER SIZE OF PAGE FRAME:");
   scanf("%d",&size_frame);

   printf("\n Page Frame:\n");

   for(i=0;i<n_pages;i++)
   printf("%d ",page_str[i]);

   printf("\nLRU PAGE REPLACEMENT ALGO:\n\n");
 for(i=0;i<n_pages;i++)
 {
    for(j=0;j<size_frame;j++)
     {
       flag1=1;
       if(page[j]==page_str[i])
	{
	  flag1=0;
	  cnt[j]=i;
	  break;
	}
     }
    if(flag1==1)
    {
	fault++;
	if(col>=size_frame)
	{
	    col=0;
	    cflag =1;
	}

      min = cnt[0];
      for(j=0;j<size_frame;j++)
      {
	   if(min > cnt[j] && cnt[j]!=-1)
	   {
		min = cnt[j];
		col = j;
	   }
	}
      if(min == cnt[0]&&cflag == 1)
	{
	   col = 0;
	}
	cnt[col]=i;
	page[col++]=page_str[i];
     }
      for(k=0;k<size_frame;k++)
      {
	 printf("  %d  ",page[k]);

      }
      printf("\n\n");
  }
  printf("\nNo of Faults :%d",fault);

}

void optimal()

{
	int p[30],i,j,fs[3],no_of_pages,size_frame,max,
	found=0,lg[3],index,k,l,flag1=0,flag2=0,pf=0,
	fr[10]={-1,-1,-1};
	printf("20\n7 0 1 2 0 3 0 4 2 3 0 3 2 1 2 0 1 7 0 1\n");
	printf("\nENTER NO PAGES IN REFERENCE STRING::->");
	scanf("%d",&no_of_pages);
	printf("\nENTER %d PAGE NO.S::->",no_of_pages);
	for(i=0;i<no_of_pages;i++)
	scanf("%d,",&p[i]);
	printf("\nENTER SIZE OF PAGE FRAME:");
	scanf("%d",&size_frame);
	printf("\n");
	for(j=0;j<no_of_pages;j++)
	 {
	  flag1=0;
	  flag2=0;
	  for(i=0;i<size_frame;i++)
	  {
	    if(fr[i]==p[j])
	     {
	      flag1=1;
	      flag2=1;
	      break;
	     }
	   }
	   if(flag1==0)
	    {
	     for(i=0;i<size_frame;i++)
	      {
	       if(fr[i]==-1)
		{
		 fr[i]=p[j];
		 flag2=1;
		 pf++;
		 break;
		}
	      }
	    }
	   if(flag2==0)
	    {
	     for(i=0;i<size_frame;i++)
	      lg[i]=0;
	      for(i=0;i<size_frame;i++)
	       {
		for(k=j+1;k<no_of_pages;k++)
		 {
		  if(fr[i]==p[k])
		   {
		    lg[i]=k-j;
		    break;
		   }
		 }
	       }
	       found=0;
	       for(i=0;i<size_frame;i++)
		{
		 if(lg[i]==0)
		  {
		   index=i;
		   found=1;
		   break;
		  }
		}
	       if(found==0)
		{
		 max=lg[0];
		 index=0;
		 for(i=1;i<size_frame;i++)
		  {
		   if(max<lg[i])
		    {
		     max=lg[i];
		     index=i;
		    }
		  }
		}
	       fr[index]=p[j];
	       pf++;
	   }
	   for(k=0;k<size_frame;k++)
	    printf("  %d  ",fr[k]);
	   printf("\n");
	 }
	printf("\nNO.OF PAGE FAULTS:- %d",pf);

 }
