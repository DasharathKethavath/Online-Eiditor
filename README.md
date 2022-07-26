// Online C# Editor for free
// Write, Edit and Run your C# code using C# Online Compiler

using System;

public class HelloWorld
{
     static int m2, d2;
    public static void Main(string[] args)
    {
        Console.WriteLine ("Enter the date format dd/mm/yyyy");
        string dateformat = Console.ReadLine();
        string day = dateformat.Substring(0,2);
        string month = dateformat.Substring(3,2);
        string year = dateformat.Substring(6,4);
        Console.WriteLine("please enter add days");
        string days = Console.ReadLine();
        string result = addDays(Convert.ToInt32(day),Convert.ToInt32(month),Convert.ToInt32(year),Convert.ToInt32(days));
        Console.WriteLine(result);
    }
    
    static string addDays(int d1, int m1, int y1, int x)
{
    int offset1 = offsetDays(d1, m1, y1);
    int remDays = isLeap(y1) ? (366 - offset1) : (365 - offset1);
 
    // y2 is going to store result year and
    // offset2 is going to store offset days
    // in result year.
    int y2, offset2 = 0;
    if (x <= remDays)
    {
        y2 = y1;
        offset2 = offset1+x;
    }
 
    else
    {
        // x may store thousands of days.
        // We find correct year and offset
        // in the year.
        x -= remDays;
        y2 = y1 + 1;
        int y2days = isLeap(y2) ? 366 : 365;
        while (x >= y2days)
        {
            x -= y2days;
            y2++;
            y2days = isLeap(y2)?366:365;
        }
        offset2 = x;
    }
    revoffsetDays(offset2, y2);
    string res = d2+"/"+m2+"/"+"/"+y2;
   return res;
}
static bool isLeap(int y)
{
    if (y % 100 != 0 && y % 4 == 0 || y % 400 == 0)
        return true;
 
    return false;
}
 
// Given a date, returns number of days elapsed
// from the beginning of the current year (1st
// jan).
static int offsetDays(int d, int m, int y)
{
    int offset = d;
 
    if(m - 1 == 11)
        offset += 335;
    if(m - 1 == 10)
        offset += 304;
    if(m - 1 == 9)
        offset += 273;
    if(m - 1 == 8)
        offset += 243;
    if(m - 1 == 7)
        offset += 212;
    if(m - 1 == 6)
        offset += 181;
    if(m - 1 == 5)
        offset += 151;
    if(m - 1 == 4)
        offset += 120;
    if(m - 1 == 3)
        offset += 90;
    if(m - 1 == 2)
        offset += 59;
    if(m - 1 == 1)
        offset += 31;
 
    if (isLeap(y) && m > 2)
        offset += 1;
 
    return offset;
}
 
// Given a year and days elapsed in it, finds
// date by storing results in d and m.
static void revoffsetDays(int offset, int y)
{
    int []month = { 0, 31, 28, 31, 30, 31, 30,
                    31, 31, 30, 31, 30, 31 };
 
    if (isLeap(y))
        month[2] = 29;
    int i;
    for (i = 1; i <= 12; i++)
    {
        if (offset <= month[i])
            break;
        offset = offset - month[i];
    }
 
    d2 = offset;
    m2 = i;
}
 
}
