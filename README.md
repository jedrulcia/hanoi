Hi. This is my C# code that helps solving the Tower of Hanoi game with the lowest possible number of moves. User just needs to type in the number of the moves and the instruction will pop.





using System;
using System.Numerics;
using System.Security.Cryptography.X509Certificates;

namespace Hanoi
{
    internal class Program
    {
        static void Main(string[] args)
        {
            Console.Write("Type the number of the disks: ");
            int n = Convert.ToInt32(Console.ReadLine());
            Hanoi(n);
        }

        static void Hanoi(int n)
        {
            int moves = CountingTheMoves(n);
            int[] t0 = CreatingTab(n);
            int[] t1 = new int[0];
            int[] t2 = new int[0];
            int a = 0, b = 1, c = 2, x = 0;
            if (n % 2 == 0)
            {
                for (int move = 1; move <= moves; move++)
                {
                    if (move % 3 == 0) MovingTheDisk(ref t1, ref t2, '1', '2', move);
                    else if (move % 3 == 1) MovingTheDisk(ref t0, ref t1, '0', '1', move);
                    else MovingTheDisk(ref t0, ref t2, '0', '2', move);
                }
            }
            else
            {
                for (int move = 1; move <= moves; move++)
                {
                    if (move % 3 == 0) MovingTheDisk(ref t1, ref t2, '1', '2', move);
                    else if (move % 3 == 1) MovingTheDisk(ref t0, ref t2, '0', '2', move);
                    else MovingTheDisk(ref t0, ref t1, '0', '1', move);
                }
            }
        }

        static int CountingTheMoves(int n)
        {
            int sum = 1;
            while (n > 0)
            {
                sum = sum * 2;
                n--;
            }
            return sum - 1;
        }

        static int[] CreatingTab(int n)
        {
            int[] t0 = new int[n];
            for (int x = 0; n > 0; x++, n--) t0[x] = n;
            return t0;
        }

        static (int[], int[]) MovingTheDisk(ref int[] ta, ref int[] tb, char a, char b, int move)
        {
            int n = 0;
            if (tb.Length == 0 || (ta.Length != 0 && ta[ta.Length - 1] < tb[tb.Length - 1]))
            {
                Console.WriteLine(move + ": Move the disk from stack " + a + " to stack " + b);
                Array.Resize<int>(ref tb, tb.Length + 1);
                tb[tb.Length - 1] = ta[ta.Length - 1];
                Array.Resize<int>(ref ta, ta.Length - 1);
            }
            else
            {
                MovingTheDisk(ref tb, ref ta, b, a, move);
                n++;
            }
            if (n == 0) return (ta, tb);
            return (tb, ta);
        }
    }
}

