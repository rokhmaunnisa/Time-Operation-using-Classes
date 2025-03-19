#include<iostream>
using namespace std;

class Time{
    private:
        int hrs,mins,secs;
    public:
        //default constructor
        Time(){
            hrs = 0;
            mins = 0;
            secs = 0;
        }
        //parametrized constructor
        Time(int h,int m,int s){
            hrs = h;
            mins = m;
            secs = s;
        }
        //method which instantiates Time properties
        void SetTime(int h,int m,int s){
            hrs = h;
            mins = m;
            secs = s;
        }
        //method display time
        void DisplayTime(){
            cout<<endl<<hrs<<":"<<mins<<":"<<secs<<endl;
        }
        //function to normalize the time
        void timeNormalize(int op){
            if(op == 1){
                mins = mins + (secs/60);
                secs = secs % 60;
                hrs = hrs + (mins/60);
                mins = mins % 60;
            }
            else{
                mins = mins - (secs/60);
                secs = secs % 60;
                hrs = hrs - (mins/60);
                mins = mins % 60;
            }
        }
        //+ operator overloading
        Time operator +(Time t){
            Time tempTime;
            tempTime.secs = secs + t.secs;
            tempTime.mins = mins + t.mins;
            tempTime.hrs = hrs + t.hrs;
            tempTime.timeNormalize(1);
            return (tempTime);
        }
        //- operator overloading
        Time operator -(Time t){
            Time tempTime2;
            tempTime2.secs = secs - t.secs;
            tempTime2.mins = mins - t.mins;
            tempTime2.hrs = hrs - t.hrs;
            tempTime2.timeNormalize(2);
            return (tempTime2);
        }
};

int main(){
    Time t[3],result,tFinal;
    for(int i=0;i<3;i++){
        int h,m,s;
        cout<<"Time - "<<i+1<<endl;
        cout<<"Enter Hours: ";
        cin>>h;
        cout<<"Enter Minutes: ";
        cin>>m;
        cout<<"Enter Seconds: ";
        cin>>s;
        t[i].SetTime(h,m,s);
    }
    //5:50:30 + 7:20:34 = 13:11:4
    result = t[0] + t[1];
    //20:20:34 - 13:11:4 = 7:9:30
    tFinal = t[2] - result;

    t[0].DisplayTime();cout<<ends<<" + ";t[1].DisplayTime();cout<<ends<<" = ";result.DisplayTime();

    t[2].DisplayTime();cout<<ends<<" - ";result.DisplayTime();cout<<ends<<" = ";tFinal.DisplayTime();

    return 0;
}
