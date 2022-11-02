# 13-CODEOLOGIST
LIBRARY MANAGEMENT SYSTEM 
#include <iostream>
#include <cstring>
#include <string.h>
#include <malloc.h>
#define issuemax 100
using namespace std;

class issue
{
	public:
		issue()
		{
			return_status = 0;
		}
		int return_copy()
		{
			return copies;
		}
	private:
		int id;
		char bname;
		int copies;
		int period;
		struct doi{
			int day;
			int month;
			int year;
		}d;
		struct dor{
			int day;
			int month;
			int year;
		}r;
		int return_status;
		
		
	public:
		void get_issue_details(int cop)
		{
			copies = cop;
			cout<<"Enter the id: ";
			cin>>id;
			cout<<"Enter the issue day: ";
			cin>>d.day;
			cout<<"Enter the issue month: ";
			cin>>d.month;
			cout<<"Enter the issue year: ";
			cin>>d.year;
		}
		void display()
		{
			cout<<"Issue id: "<<id<<endl;
			cout<<"Issued number of copies: "<<copies<<endl;
			cout<<"Date of issue "<<d.day<<"/"<<d.month<<"/"<<d.year<<endl;
			if(return_status = 1)
			{
				cout<<"Return date "<<r.day<<"/"<<r.month<<"/"<<r.year<<endl;
			}
		}
		int return_id()
		{
			return id;
		}
};


class books
{
	private:
		char bname[50];
		char author[50];
		int total_available;
		int total_rented;
		
		public:
			void get_details()
			{
				cout<<"Enter the name of the book: ";
				cin>>bname;
				cout<<"Enter the author of the book: ";
				cin>>author;
				cout<<"Enter the total number of available book: ";
				cin>>total_available;
				cout<<"Enter the total number of rented book: ";
				cin>>total_rented;
				cout<<endl<<endl;;
			}
			
			void display()
			{
				cout<<"Book Name: "<<bname<<endl;
				cout<<"Author : "<<author<<endl;
				cout<<"Total Available books :"<<total_available<<endl;
				cout<<"Total Rented book :"<<total_rented<<endl;
				cout<<"Total book owned by library";
				cout<<endl<<endl;;
			}
			
			
			int rent_request(char booktitle[50], char book_author[50], int copies)
			{
				if((strcmp(bname, booktitle) == 0) && (strcmp(author, book_author) == 0) && (total_available>=copies))
				{
					return 1;
				}
				else if((strcmp(bname, booktitle) == 0) && (strcmp(author, book_author) == 0))
				{
					return 2;
					
				}
				else
				{
					return 0;
				}
			}
			
			void rent(int rent_copies)
			{
				total_available = total_available - rent_copies;
				total_rented = total_rented + rent_copies;
			}
			
			void return_book(int rent_copies)
			{
				total_available = total_available + rent_copies;
				total_rented = total_rented - rent_copies;
			}
			
			int search(char booktitle[50], char book_author[50])
			{
				if((strcmp(bname, booktitle) == 0) && (strcmp(author, book_author) == 0))
				{
					return 1;
				}
				else
				{
					return 0;
				}
			}
};
class books *b;
class issue issue_details[issuemax];
int total_issues = -1;
static int book_count = 0;

int main()
{
	b = (class books *) (malloc(sizeof(class books)));
	int option_main, manager_id, manager_password;
	manager_id = 777;
	manager_password = 777;
	int m_id, m_password;
	do
	{
		cout<<"\n\t\tWelcome to the library management system."<<endl;
		cout<<"Please choose one of the option below: "<<endl;
		cout<<"Enter 1 to access student library portal."<<endl;
		cout<<"Enter 2 to access adminstration management portal."<<endl;
		cout<<"Enter -1 to exit"<<endl;
		cout<<"Enter your option here: ";
		cin>>option_main;
		cout<<endl;
		switch(option_main)
		{
			case -1:{
				break;
			}
			case 1:{
				int option_student;
				do{
					cout<<"Enter 1 to display all book details."<<endl;
					cout<<"Enter 2 to search a book."<<endl;
					cout<<"Enter 3 to rent a book."<<endl;
					cout<<"Enter 4 to return the book: "<<endl;
					cout<<"Enter your option here: ";
					cin>>option_student;
					
					switch(option_student)
					{
						case -1:
							{
								break;
							}
						case 1:{
							for(int i = 1; i<=book_count; i++)
							{
								b[i].display();
							}
							break;
						}
						case 2:{
							int flag;
							char s_b_n[50];
							char s_b_a[50];
							cout<<"Enter the book name to search: ";
							cin>>s_b_n;
							cout<<"Enter the book author name: ";
							cin>>s_b_a;
							int i;
							for(i = 1; i<=book_count; i++)
							{
								flag = b[i].search(s_b_n, s_b_a);
								if(flag == 1)
								{
									break;
								}
							}
							b[i].display();
							if(flag == 0)
							{
								cout<<"The searched book was not found in the database."<<endl;
							}
							cout<<endl;
							break;
						}
						case 3:
							{
							int flag;
							char s_b_n[50];
							char s_b_a[50];
							int cop_req;
							cout<<"Enter the book name to search: ";
							cin>>s_b_n;
							cout<<"Enter the book author name: ";
							cin>>s_b_a;
							cout<<"Enter the number of copies to rent: ";
							cin>>cop_req;
							int i;
							for(i = 1; i<=book_count; i++)
							{
								flag = b[i].rent_request(s_b_n, s_b_a, cop_req);
								if(flag == 1 || 2)
								{
									break;
								}
							}
							if(flag == 1)
							{
								b[i].rent(cop_req);
								issue_details[total_issues].get_issue_details(cop_req);
								cout<<"Rent Request Processed successfully"<<endl;
							}
							else if(flag == 2)
							{
								cout<<"Sorry the book is not available in the requested number of copies."<<endl;
							}
							else
							{
								cout<<"Sorry the book was not found in the database.";
							}
							cout<<endl;
							break;
							}
							case 4:
								{
								int flag;
								char s_b_n[50];
								char s_b_a[50];
								int period;
								cout<<"Enter the book name to search: ";
								cin>>s_b_n;
								cout<<"Enter the book author name: ";
								cin>>s_b_a;
								cout<<"Enter the number of days of rented book: ";
								cin>>period;
								int i;
								for(i = 1; i<=book_count; i++)
								{
									flag = b[i].search(s_b_n, s_b_a);
									if(flag == 1)
									{
										break;
									}
								}
								int t_id;
								int flag2;
								cout<<"Enter the issue id: ";
								cin>>t_id;
								int j;

								for(j = 0; j<total_issues; j++)
								{
									if(t_id == issue_details[j].return_id());
									{
										break;
										flag2 = 1;
									}
									issue_details[j].display();
								}
								b[i].return_book(issue_details[j].return_copy());
								if(period <=15)
								{
									cout<<"There is no fine for the rent"<<endl;
								}
								else if(period>15 && period<30)
								{
									cout<<"The fine for the rent is: "<<((period-15)*5);
								}
								else
								{
									cout<<"The fine for the rent is: "<<((period-30)*10);
								}

							}
							cout<<endl;
					}

				}
				while(option_student != -1);
		
	}
		
			case 2:{
				cout<<"Enter the manager id: ";
				cin>>m_id;
				cout<<"Enter the admin password to continue: ";
				cin>>m_password;
				if(m_id == manager_id && m_password == manager_password)
				{
					cout<<"Welcome to the Admin Portal"<<endl;
					
					int option_admin;
					do{
						cout<<"Enter 1 to add books to database."<<endl;
						cout<<"Enter 2 to display all book details."<<endl;
						cout<<"Enter 3 to search a book."<<endl;
						cout<<"Enter 4 to search a issue."<<endl;
						cout<<"Enter your option here: ";
						cin>>option_admin;
						
						switch(option_admin)
						{
							case -1:
							{
								break;
							}
							case 1:
							{
								book_count++;
								b = (class books *)(realloc(b, book_count*sizeof(class books)));
								b[book_count].get_details();
								cout<<endl;
								break;
							}
							case 2:
								{
									for(int i = 1; i<=book_count; i++)
									{
										b[i].display();
									}
									break;
								}
							case 3:
								{
									int flag;
									char s_b_n[50];
									char s_b_a[50];
									cout<<"Enter the book name to search: ";
									cin>>s_b_n;
									cout<<"Enter the book author name: ";
									cin>>s_b_a;
									int i;
									for(i = 1; i<=book_count; i++)
									{
										flag = b[i].search(s_b_n, s_b_a);
										if(flag == 1)
										{
											break;
										}
									}
									b[i].display();
									if(flag == 0)
									{
										cout<<"The searched book was not found in the database."<<endl;
									}
									break;
									
								}
							case 4:
								{
									int t_id;
									int flag;
									cout<<"Enter the issue id: ";
									cin>>t_id;
									int i;
									
									for(i = 0; i<total_issues; i++)
									{
										if(t_id == issue_details[i].return_id());
										{
											break;
											flag = 1;
										}
										issue_details[i].display();
									}
									if(flag == 0)
									{
										cout<<"The searched issue is not in the database."<<endl;
									}
									break;
									cout<<endl;
								}
							default:{
								cout<<"Please enter a valid option"<<endl;
								break;
							}
							
						}
						
					}
					while(option_admin != -1 );
					
				}
				else
				{
					cout<<"The entered id or password is wrong. Please try again.";
				}
				break;
			}
			cout<<endl<<endl;
		}
	}
while(option_main!= -1);
}
