# Searching-for-Patterns
Searching for patterns using (Boyer Moore) Algorithm
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.IO;

namespace ConsoleApplication115
{


    public class BoyerMoore
    {
        private String str1;
        private String str2;
        private int length1;
        private int length2;

        public BoyerMoore()
        {
            str1 = null;
            str2 = null;
            length1 = 0;
            length2 = 0;

        }

        public void Insert(String s1, String s2)
        {
            this.str1 = s1;
            this.str2 = s2;
            this.length1 = s1.Length;
            this.length2 = s2.Length;
        }

        public void BoyerMooreMatching()
        {
            int occur = 0, comp = 0, k = 0, i = 0, j = 0, flag = 0, flag2 = 0, temp = 0, foo = 0;

            while ((i < length1) && (i + length2 < length1))
            {
                flag = 0; temp = 0;
                for (j = length2 - 1; j >= 0; j--)
                {
                    if (str1[i + j] == str2[j])
                    {
                        comp++;
                        flag = 1;
                    }
                    else
                    {
                        comp++;
                        flag = 0;
                        temp = j + i;
                        break;
                    }
                }
                if (flag == 0)
                {

                    flag2 = 0; foo = 0;
                    for (k = j - 1; k >= 0; k--)
                    {
                        if (str2[k] == str1[temp])
                        {
                            i = i + foo;
                            flag2 = 1;
                            break;
                        }
                        else
                        {
                            foo++;
                            flag2 = 0;
                        }
                    }
                    if (flag2 == 0)
                    {
                        i = i + (length2);
                    }
                }
                else if (flag == 1)
                {
                    occur++;
                    Console.WriteLine("Pattern found at index " + i);
                }
                i++;
            }

            if (occur > 0)
            {
                Console.WriteLine("Pattern matched " + occur + " times!");
            }

            Console.WriteLine("Total comparisions: " + comp);
        }


    }

    class Program
    {
        static void Main(string[] args)
        {
            StreamReader pobj = new StreamReader("C://Users//Desktop//ALGOP.txt");
            StreamReader obk = new StreamReader("C://Users//Desktop//ALGO.txt");
            BoyerMoore obj = new BoyerMoore();
            String s1;
            s1 = pobj.ReadLine();
            String s2;
            s2 = obk.ReadLine();
            Console.WriteLine("\nText: " + s1);
            Console.WriteLine("\nPattern: " + s2 + "\n");
            Console.WriteLine("Length of Text: " + s1.Length);
            Console.WriteLine("Length of pattern: " + s2.Length);
            obj.Insert(s1, s2);
            obj.BoyerMooreMatching();
            Console.ReadLine();
        }
    }
}
