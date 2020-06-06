using System;

namespace CowsAndBulls 
{
    class Program
    {
        static void Main(string[] args)
        {
            int generatedNumber = GenerateNumber();
            Console.WriteLine("   * Bulls and Cows Game *  \n");
            Console.WriteLine("The computer has picked a number!\nTry to guess it.\n");

            int[] numbersArr = new int[4];
            int temp = generatedNumber; 
            for (int i = 3; i >= 0; i--)
            {
                numbersArr[i] = temp % 10;
                temp /= 10;
            }

            for (int i = 0; i < 100; i++)
            {
                Console.Write("Guess: ");
                string text = Console.ReadLine();
                int number = Convert.ToInt32(text);

                if (!IsNumberValid(number))
                {
                    Console.WriteLine("Invalid number.Try again.");
                    continue;
                }

                if (CheckBulls(generatedNumber, number) == 4)
                {
                    Console.WriteLine("Result: 4 Bulls!");
                    break;
                }

                Console.Write("Result: ");
                Console.Write(CheckBulls(number, generatedNumber));
                Console.Write(" Bulls, ");
                Console.Write(CheckCows(number, numbersArr));
                Console.Write(" Cows\n");

            }
        }

        private static int GenerateNumber()
        {
            Random num = new Random();

            int digit1, digit2, digit3, digit4;

            digit1 = num.Next(1, 10);

            do
            {
                digit2 = num.Next(0, 10);
            } while (digit1 == digit2);

            do
            {
                digit3 = num.Next(0, 10);
            } while (digit3 == digit1 || digit3 == digit2);

            do
            {
                digit4 = num.Next(0, 10);
            } while (digit4 == digit1 || digit4 == digit2 || digit4 == digit3);

            int number;
            number = digit1 * 1000 + digit2 * 100 + digit3 * 10 + digit4;

            return number;
        }

        private static int CheckBulls(int number, int generatedNumber)
        {
            int countBulls = 0;
            for (int i = 0; i < 4; i++)
            {

                if (number % 10 == generatedNumber % 10)
                {
                    countBulls++;
                }

                number /= 10;
                generatedNumber /= 10;
            }

            return countBulls;
        }

        private static int CheckCows(int number, int[] numbersArr)
        {
            int countCows = 0;
            int digit;


            for (int i = 0; i < 4; i++)
            {

                digit = number % 10;

                if (i == 0)
                {
                    if (digit == numbersArr[0] || digit == numbersArr[1] || digit == numbersArr[2])
                    {
                        countCows++;
                    }
                }
                else if (i == 1)
                {
                    if (digit == numbersArr[0] || digit == numbersArr[1] || digit == numbersArr[3])
                    {
                        countCows++;
                    }
                }
                else if (i == 2)
                {
                    if (digit == numbersArr[0] || digit == numbersArr[2] || digit == numbersArr[3])
                    {
                        countCows++;
                    }
                }
                else if (i == 3)
                {
                    if (digit == numbersArr[1] || digit == numbersArr[2] || digit == numbersArr[3])
                    {
                        countCows++;
                    }
                }

                number /= 10;
            }

            return countCows;
        }
        private static int countDigits(int num)
        {

            int counter = 0;
            while (true)
            {

                counter++;
                num = num / 10;
                if (num == 0)
                {
                    break;
                }
            }
            return counter;
        }

        private static bool IsNumberValid(int number)
        {

            if (countDigits(number) != 4)
            {
                return false;
            }

            int digit1, digit2, digit3, digit4;

            digit4 = number % 10;
            number /= 10;
            digit3 = number % 10;
            number /= 10;
            digit2 = number % 10;
            number /= 10;
            digit1 = number % 10;

            if (digit1 == '0')
            {
                return false;
            }
            else if (digit1 == digit2 || digit1 == digit3 || digit1 == digit4 || digit2 == digit3 || digit2 == digit4 || digit3 == digit4)
            {
                return false;
            }

            return true;
        }

    }
}
