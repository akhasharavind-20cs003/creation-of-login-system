#include <stdio.h>
#include <string.h>
#include <stdlib.h>

struct login
{
    char name[30];
    int age;
    char gender[10];
	char DOB[10];
    char pnum[10];
    char Bgroup[10];
    char aadhar[20];
    char address[30];
    char mail[20];
    char qual[10];
    char username[30];
    char password[20];
};

void login (void);
void registration (void);
void deletion(void);

int main (void)
{
    int option;

    printf("Press '1' to Register\nPress '2' to Login\nPress '3' to Delete your account\n");
    scanf("%d",&option);

    getchar();

    if(option == 1)
        {
            system("CLS");
            registration();
        }

    else if(option == 2)
        {
            system("CLS");
            login();
        }
    else if(option == 3)
	{
	       system("CLS");
	       deletion();
	}
}

void login (void)
{
    char username[30],password[20];
    FILE *log;
    int found =0;
    log = fopen("login.txt","r");
    if (log == NULL)
    {
        fputs("Error at opening File!", stderr);
        exit(1);
    }

    struct login l;

    printf("\nPlease Enter your login credentials below\n\n");
    printf("Username:  ");
    gets(username);
    printf("\nPassword: ");
    printf("\n");
    gets(password);

    while(fread(&l,sizeof(l),1,log))
        {

        if(strcmp(username,l.username)==0 && strcmp(password,l.password)==0)

            {
                printf("\nSuccessful Login\n");
                found =1;

            }
        }
        if(!found)
            {
                printf("\nIncorrect Login Details\nPlease enter the correct credentials\n");
            }

    fclose(log);
    return;
}




void registration(void)
{
    char name[15];
    FILE *log;

    log=fopen("login.txt","a");
    if (log == NULL)
    {
        fputs("Error at opening File!", stderr);
        exit(1);
    }


    struct login l;

    printf("\nWelcome to your online course provider. We need to enter some details for registration.\n\n");
    printf("\nEnter your Name:\n");
    scanf("%s",l.name);
    printf("\nEnter your age:\n");
    scanf("%d",&l.age);
    printf("\nEnter your Gender:\n");
    scanf("%s",l.gender);
    printf("\nEnter your DOB:\n");
    scanf("%s",l.DOB);
    printf("\nEnter your Qualification:\n");
    scanf("%s",l.qual);
	printf("\nEnter your Phone number:\n");
    scanf("%s",l.pnum);
    printf("\nEnter your Blood Group:\n");
    scanf("%s",l.Bgroup);
    printf("\nEnter your Aadhar number:\n");
    scanf("%s",l.aadhar);
    printf("\nEnter your Address:\n");
    scanf("%s",l.address);
    printf("\nEnter your email address\n");
	scanf("%s",l.mail);
    
    printf("Thank you.\nNow please choose a username and password as credentials for system login.\nEnsure the username is no more than 6 characters long.\nEnsure your password is at least 8 characters.\n");

    printf("\nEnter Username:\n");
    scanf("%s",l.username);
    printf("\nEnter Password:\n");
    scanf("%s",l.password);
    fwrite(&l,sizeof(l),1,log);
    fclose(log);
	getchar();
    system("CLS");
	printf("\nConfirming details...\n...\nWelcome, %s!\n\n",l.name);
    printf("\nRegistration Successful!\n");
    printf("Press any key to continue...");

   }
   void deletion(void){

	char username[30],password[20];
    FILE *log,*temp;
    int found =0;
    log = fopen("login.txt","r");
    temp=fopen("Temp.txt","w");
    if (log == NULL)
    {
        fputs("Error at opening File!", stderr);
        exit(3);
    }

    struct login l;

    printf("\nPlease enter Username and Password to delete your account\n\n");
    printf("Username:  ");
    gets(username);
    printf("\nPassword: ");
    gets(password);
    while(fread(&l,sizeof(l),1,log)){
     if(strcmp(username,l.username)==0 && strcmp(password,l.password)==0){
        found =1;
	     printf("Your account have been removed successfully");}
	 else{
        fwrite(&l,sizeof(l),1,temp);
          }
    }
    fclose(log);
    fclose(temp);
    if(!found){
        printf("\nError while Deletion");
    }
    remove("login.txt");
    rename("Temp.txt","login.txt");
     getch();

    return;
    }

      
