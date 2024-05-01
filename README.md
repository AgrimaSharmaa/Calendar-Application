# Calendar-Application
In this project, you can view all your important dates using a fantastic and very simple Calendar written in C++.

#include<iostream>
#include <iomanip>
using namespace std;
int get_1st_weekday(int year){  //to return the starting day of the month, if it return 0 means sun is the starting day, if 1 then mon and so on
  int d;
  d = (((year - 1) * 365) + ((year - 1) / 4) - ((year - 1) / 100) + ((year) / 400) + 1) % 7;
  return d;
}
int main()
{
   int year,month,day,daysInMonth,weekDay=0,startingDay;
   cout<<"Enter your desired year:";
   cin>>year;

   string months[]={"January","February","March","April","May","June","July","August","September","October","November","December"};
   int monthDay[]={31,28,31,30,31,30,31,31,30,31,30,31};   //number of days in each month of a non-leap year

   if((year%4==0&&year%100!=0)||year%400==0) { //number of days in case of leap year
       monthDay[1]=29;
   }

   startingDay=get_1st_weekday(year);  //call the function

   for(month=0;month<12;month++){    //to print the names of the months

      daysInMonth=monthDay[month];   //to access the number of days in corresponding months
      cout<<"\n\n------------------------------------------\n"<<months[month];
      cout<<"\n  Sun  Mon  Tue  Wed  Thurs  Fri  Sat\n";   //to print the names of the months

      for(weekDay=0;weekDay<startingDay;weekDay++)   //until the first day of a month is just next to the last day of the previous month, we need blank spaces on the previous days  
        cout<<"     ";

      for(day=1;day<=daysInMonth;day++){    //to print the days in month
        cout<<setw(5)<<day;

        if(++weekDay>6){  //weekDay is days of week like sun,  mon etc, after 0 to 6(sun to sat), sun should be repeated
            cout<<"\n";  //Move to new line
            weekDay=0;  //and return to  sun 
        }
        startingDay=weekDay;
      }

   }

return 0;
}
