#include<iostream>
 #include<fstream>
 using namespace std;
 typedef struct student
 {
 int roll;
 char a,name[20],add[30];
 }stud;
 ifstream fin;
 ofstream fout;
 fstream fm;
 int n;
 char fname[20];
 void create();
 void display();
 void insert();
 void search(int key);
 void delete1(int key);
 int main()
 {
 int ch,x;
 do
 {
 cout<<"\n1.Accept\n2.Display\n3.Insert\n4.Search\n5.Delete\n6.Exit";
 cout<<"\nEnter your choice=";
 cin>>ch;
 switch(ch)
 {
 case 1:
 create();
 break;
 case 2:
 display();
 break;
 case 3:
 insert();
 break;
 case 4: 
cout<<"Enter roll no to search=";
 cin>>x;
 search(x);
break;
 case 5:
 cout<<"Enter roll no to delete=";
 cin>>x;
 delete1(x);
 break;
 }
 }while(ch!=6);
 return 0;
 }
 void create()
 {
 int i;
 stud s;
 cout<<"Enter name of the file=";
 cin>>fname;
 fm.open(fname,ios::out);
 cout<<"\nEnter no. of records:=";
 cin>>n;
 for(i=0;i<n;i++)
 {
 cout<<"Enter roll no=";
 cin>>s.roll;
 cout<<"Enter name=";
 cin>>s.name;
 cout<<"Enter division=";
 cin>>s.a;
 cout<<"Enter address=";
 cin>>s.add;
 fm.write((char*)&s,sizeof(s));
 }
 fm.close();
 }//create
 void display()
 {
 int i;
 stud s;
 fin.open(fname);
 cout<<"\nROLL NO\tNAME\tDIV\tADDRESS";
     //
 while(!fin.eof())
 for(i=0;i<n;i++)
{
 fin.read((char*)&s,sizeof(s));
 cout<<"\n"<<s.roll<<"\t"<<s.name<<"\t"<<s.a<<"\t"<<s.add;
 }
 fin.close();
 }//display
 void insert()
 {
 stud s;
 fout.open(fname,ios::app);
 cout<<"Enter roll no=";
 cin>>s.roll;
 cout<<"Enter name=";
 cin>>s.name;
 cout<<"Enter division=";
 cin>>s.a;
 cout<<"Enter address=";
 cin>>s.add;
 fout.write((char*)&s,sizeof(s));
 n++;
 fout.close();
 }
 void search(int key)
 {  
stud s;
 int flag=0,i;
 fin.open(fname);
 for(i=0;i<n;i++)
 {
    fin.read((char *)&s,sizeof(s));
    if(s.roll==key)
    {
 cout<<"\nRecord is present"; 
cout<<s.roll<<"\nRoll No.";
 cout<<s.name<<"\nName=";
 cout<<s.a<<"\nDivision=";
 cout<<s.add<<"\nAddress=";
 flag=1;
    }
 }
 if(flag==0)
 cout<<"\nRoll no.= "<<key<<" is not present in the record";
}
     fin.close();
 void delete1(int key)
 {  
stud s;
 int flag=0,i;
 fin.open(fname);
 fout.open("temp.txt",ios::out);
 for(i=0;i<n;i++)
 {
 fin.read((char *)&s,sizeof(s));
 if(s.roll==key)
 {   
cout<<"\nRecord deleted successfully";
 flag=1;
 }
 else
 {
 }
 }
 if(flag==0)
 fout.write((char *)&s,sizeof(s));
 cout<<"\nRoll no.= "<<key<<" is not present in the record";
 else
 n--;
 fin.close();
 fout.close();
 remove(fname);
 rename("temp.txt",fname);
 
