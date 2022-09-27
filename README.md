# subhamcolor

#include <stdio.h>
#include <conio.h>
#include <windows.h>
#include <string.h>
void menu();
void namefun();
void searchfun();
void listfun();
void updatefun();
void deletefun();
void exitfun();
void login();
void account();
void accountcreated();
struct userpass 
{
	char password[50];
	char username[50];
};
main()
{
	system("color 5");
	
		int cho;
		
		
	      printf("\t\t************************ WELCOME TO PHONEBOOK DIRECTORY ****************************************");
	      printf("\nPRESS '1' FOR SIGN UP -- \nPRESS'2' FOR SIGN IN--\n");
	      scanf("%d",&cho);
	      if(cho==1)
	      {
		     system("cls");
		     account();
	      }
	        else if(cho==2)
	        {
		       system("CLS");
		        login();
	       }	     	
}
void login()
{
	system("cls");

	char username[50];
	char password[50];

	int i, j, k;
	char ch;
	FILE *fc;
    struct userpass u1 ;

	fc = fopen("username.txt","rb");

	if (fc == NULL) 
	{
		printf("\t\t\t ERROR IN OPENING FILE\n\n");
	}

	printf("\t\t\tACCOUNT LOGIN\n\n ");
	
	
	printf("\t\t\t***********************************************"
	       "********************************\n\n");


	printf("\t\t\t==== LOG IN ====\n\n");

	// Take input

	printf("\t\t\tUSERNAME..");
	scanf("%s", &username);


	printf("\t\t\tPASSWORD..");

	// Input the password
	for (i = 0; i < 50; i++) 
	{
		ch = getch();
		if (ch!= 13)
	    {
			password[i] = ch;
			ch = '*';
			printf("%c",ch);
			fflush(stdin); 
		}
		else
		break;
	}
	while (fread(&u1, sizeof(u1),1,fc))
	{
		if (strcmp(username,u1.username)==0)
		{
			menu();
		}
	}
	fclose(fc);
}

void account()
{
	char password[20];
	int passwordlength, i, seek = 0;
	char ch;
	FILE *fp;
	struct  userpass u1;
	 //struct userpass ;

	fp = fopen("username.txt", "ab");

	// Inputs
	system("cls");
	printf("\t\t\t\t!!!!!CREATE ACCOUNT!!!!!\n\n");


	printf("\t\t\tUSERNAME..");
	scanf("%s",&u1.username);

	printf("\t\t\tPASSWORD..");
	
	for (i = 0; i < 50; i++)
	{
		ch = getch();
		if (ch != 13) 
		{
			password[i] = ch;
			ch = '*';
			printf("%c", ch);
		}
		else
		break;	
	}

	// Writing to the file
	fwrite(&u1, sizeof(u1),1, fp);
	fclose(fp);
	
	accountcreated();
}
void accountcreated()
{
	int i;
	char ch;
	system("cls");
	printf("\t\t\t\t\tPLEASE WAIT....\n\nYOUR DATA IS PROCESSING....");
	for (i = 0; i < 200000000; i++) 
	{
		i++;
		i--;
	}
	printf("\t\t\tACCOUNT CREATED SUCCESSFULLY....\n\n");

	printf("\t\t\tPress enter to login");

	getch();
	login();
}
void menu()
{
	system("cls");

	printf("\n************************ PHONEBOOK DIRECTORY ****************************************");
	
	printf("\n 1.Add New\n");
	
	printf("\n 2.Search\n");

	printf("\n 3.List\n");
	
	printf("\n 4.update\n");
	
	printf("\n 5.Delete\n");
	
	printf("\n 6.Exit\n");
	
	printf("\n 7.go Login page\n");
	switch(getch())
	{
		case '1':
			namefun();
			break;
		case '2':
			searchfun();
			break;
		case '3':
			listfun();
			break;
		case '4':
			updatefun();
			break;
		case '5':
			deletefun();
			break;
		case '6':
			exitfun();
			break;
		case '7':
		    main();	
		default:
			system("cls");
			printf("Invalid Enter.");
			getch();
   }
}

void namefun()
{
	system("cls");
	
	printf("------------------************ NEW SECTION ***********-------------------\n");
	FILE *fptr;
	char name[100];
	char address[100];
	char gmail[100];
	double phone;
	char gender[8];
	fptr=fopen("ebraj.txt","ab+");
	if(fptr==NULL)
	{
		printf("Failed to create the required file.");
	}
	else
	{
		fflush(stdin);
		printf("Name:\t");
		
		gets(name);
		
		printf("Address:\t");
	
		gets(address);
	
		printf("Gender:\t");
		
		gets(gender);
		
		printf("Gmail:\t");
		
		gets(gmail);
		
		printf("Phone Number:\t");
	
		scanf("%lf",&phone);
		fprintf(fptr,"%s %s %s %s %.0lf\n",name,address,gender,gmail,phone);
	}
	fclose(fptr);
	system("cls");
	char ch;

	printf("Do you wanna add more datas.Press y for that:");
	
	fflush(stdin);
	while((ch=getch())=='y')
	{
		menu();
	}
}

void searchfun()
{
	FILE *fptr;
	int flag=0;
	int res;
	char name[100];
	char address[100];
	char gmail[100];
	double phone;
	char gender[8];
	char name1[100];
	system("cls");
	fflush(stdin);
	printf("\n------------Enter the name of the person you want to see the detail:: ");
	gets(name1);
	fptr=fopen("ebraj.txt","r");

	while(fscanf(fptr,"%s %s %s %s %lf\n",name,address,gender,gmail,&phone)!=EOF)
	{
		res=strcmp(name,name1);
		if(res==0)
		{
			
			printf("------------****** Record Found *****-----------");
			
	
		printf("\n Name:%s",name);
		
		printf("\n Address:%s",address);
	
		printf("\n Gender:%s",gender);
		
		printf("\n Gmail:%s",gmail);
	
		printf("\n Phone Number:%.0lf",phone);
	
			printf("\n----------------------------------------");
		flag=1;
		
			printf("\nEnter y for menu option.");
        	while(getch()=='y')
	        {
		      menu();
	        }
	   }
   }
	if(flag==0)
	{
		system("cls");

		printf("\nNo record found.");
	
		printf("\nEnter a to enter file again or double y key to open menu section:");
		if(getch()=='a')
		{
			system("cls");
			searchfun();
		}
	}
	fclose(fptr);
}
void listfun()
{
	FILE *fptr;
	char name[100],address[100],gmail[100],gender[8];
	double phone;
	int f;
	fptr=fopen("ebraj.txt","r");
	system("cls");

	printf("-----------******* LIST SECTION OPENED *****---------------");
	printf("\n");
	while(fscanf(fptr,"%s %s %s %s %lf",name,address,gender,gmail,&phone)!=EOF)
	{
		
		printf("------------------------------------------\n");
		printf("Name:%s\n",name);
		printf("Address:%s\n",address);
		printf("Gender:%s\n",gender);
		printf("Gmail:%s\n",gmail);
		printf("Phone:%.0lf\n",phone);
			f=1;
				printf("------------------------------------------");
				printf("\n\n");
		}
		printf("Enter y for menu section:");
		while(getch()=='y')
		{
			menu();
		}
			fclose(fptr);
	}



void updatefun()
{
	FILE *fptr,*fptr1;
	char name[100],address[100],gmail[100],gmail1[100],address1[100],name1[100],gender[8],gender1[8];
	int res,f=0;
	int phone,phone1;
	fptr=fopen("ebraj.txt","r");
	fptr1=fopen("temp.txt","a");
	system("cls");
	printf("Enter the name: ");
	gets(name1);
	system("cls");
	while(fscanf(fptr,"%s %s %s %s %lf\n",name,address,gender,gmail,&phone)!=EOF){
		res=strcmp(name,name1);
		if(res==0)
		{
			f=1;
	
	printf("\n---------------------- SECTION OPENED --------------------");
	
			printf("\nEnter the new address:");
			scanf("%s",address1);
	
			printf("\nEnter the gender:");
			scanf("%s",gender1);

			printf("\nEnter the new gmail:");
			scanf("%s",gmail1);
			
			printf("\nEnter the new phone number:");
			scanf("%lf",&phone1);
			fprintf(fptr1,"%s %s %s %s %.0lf\n",name,address1,gender1,gmail1,phone1);	
		}
		else
		{
			fprintf(fptr1,"%s %s %s %s %.0lf\n",name,address,gender,gmail,phone);
		}
	}
	if(f==0)
	{
		printf("\t\t\tRecord Not found.");
	}
	fclose(fptr);
	fclose(fptr1);
	fptr=fopen("ebraj.txt","w");
	fclose(fptr);
	fptr=fopen("ebraj.txt","a");
	fptr1=fopen("temp.txt","r");
	while(fscanf(fptr1,"%s %s %s %s %lf\n",name,address,gender,gmail,&phone)!=EOF)
	{
		fprintf(fptr,"%s %s %s %s %.0lf\n",name,address,gender,gmail,phone);
		
	}
	fclose(fptr);
	fclose(fptr1);
	fptr1=fopen("temp.txt","w");
	fclose(fptr1);
	printf("\n\nPress y for menu option.");
	fflush(stdin);
	if(getch()=='y')
	{
		menu();
	}
}
void deletefun()
{
	FILE *fptr,*fptr1;
	char name[100],address[100],gmail[100],gmail1[100],address1[100],name1[100],gender[8];
	int res,f=0;
	int phone,phone1;
	fptr=fopen("ebraj.txt","r");
	fptr1=fopen("temp.txt","a");
	system("cls");
	printf("Enter the CONTACT name that you want to delete: ");
	gets(name1);
	system("cls");
	while(fscanf(fptr,"%s %s %s %s %lf\n",name,address,gender,gmail,&phone)!=EOF){
		res=strcmp(name,name1);
		if(res==0)
		{
			f=1;
			printf("Record deleted successfully");
			
		}
		else
		{
			fprintf(fptr1,"%s %s %s %s %.0lf\n",name,address,gender,gmail,phone);
		}
	}
	if(f==0)
	{
		printf("Record Not found.");
	}
	fclose(fptr);
	fclose(fptr1);
	fptr=fopen("ebraj.txt","w");
	fclose(fptr);
	fptr=fopen("ebraj.txt","a");
	fptr1=fopen("temp.txt","r");
	while(fscanf(fptr1,"%s %s %s %s %lf\n",name,address,gender,gmail,&phone)!=EOF)
	{
		fprintf(fptr,"%s %s %s %s %.0lf\n",name,address,gender,gmail,phone);
		
	}
	
	fclose(fptr);
	fclose(fptr1);
	fptr1=fopen("temp.txt","w");
	fclose(fptr1);
	printf("\n\nPress y for menu option.");
	fflush(stdin);
	if(getch()=='y')
	{
		menu();
	}
}
void exitfun()
{
	system("cls");
	exit;
	
}



