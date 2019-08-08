using System;
using System.Linq;

namespace RockPaperScissors
{
    class Program
    {
        static void Main(string[] args)
        {
            int score = 0;
            int roundNum = 1;
            var choice = "";
            int[] timesUsed = new int[3]; ;
            do
            {   var opponentChoice = GetRandChoice();

                do {
                    Console.WriteLine($"Round {roundNum}: rock paper or scissors?");
                    choice = Console.ReadLine(); //get user choice
                } while (!isValidChoice(choice)); // while choice is not valid repeat user entry

                Console.WriteLine($"\nYou chose {choice}, Your opponent chose {opponentChoice}");

                timesUsed[getChoiceNum(choice)]++;

            

                if (choice.Equals(opponentChoice, StringComparison.InvariantCultureIgnoreCase)) // if choices are the same it is a draw
                {
                    Console.WriteLine("Draw");
                }
                else
                {
                    switch (opponentChoice)
                    {
                        case "rock":
                            if (choice.Equals("paper", StringComparison.InvariantCultureIgnoreCase))//if user chooses paper they win the round
                            {
                                score++;
                                Console.WriteLine("Win");
                            }
                            else//else user choose scissors so they loose the round
                            {
                                score--;
                                Console.WriteLine("Loose");
                            }
                            break;
                        case "paper":
                            if (choice.Equals("scissors", StringComparison.InvariantCultureIgnoreCase))//if user chooses scissors they win the round
                            {
                                score++;
                                Console.WriteLine("Win");
                            }
                            else//else user choose rock so they loose the round
                            {
                                score--;
                                Console.WriteLine("Loose");
                            }
                            break;
                        default:
                            if (choice.Equals("rock", StringComparison.InvariantCultureIgnoreCase))//if user chooses rock they win the round
                            {
                                score++;
                                Console.WriteLine("Win");
                            }
                            else//else user choose paper so they loose the round
                            {
                                score--;
                                Console.WriteLine("Loose");
                            }
                            break;
                    }
                }



                Console.WriteLine($"The score is {score}, get a score of 3 to win the game");
                roundNum++;
             
                
            } while (score < 3 && score> -3);//if user or opponent reaches 3, end game
            if (score > 0) Console.WriteLine("\n\nCONGRATULATIONS!!!, YOU WON!!\n\n");//if user won, prints congratulations
            else Console.WriteLine("\n\nBetter luck next time.\n\n");//else print better luck next time

            Console.WriteLine($"The game lasted {roundNum-1} rounds." );
            Console.WriteLine($"You used rock {timesUsed[0]} times, paper {timesUsed[1]} times and scissors {timesUsed[2]} times");

            int maxValue = timesUsed.Max(); //gets value of largest element
          
            switch (timesUsed.ToList().IndexOf(maxValue)) { //finds index of largest value
                case 0:
                    Console.WriteLine("you used rock the most");
                    break;
                case 1:
                    Console.WriteLine("you used paper the most");
                    break;
                default:
                    Console.WriteLine("you used scissors the most");
                    break;

            }

            Console.WriteLine("Press any key to exit...");
            Console.ReadKey(true);
        }

        //gets random choice (rock, paper or scissors)
        static string GetRandChoice()
        {
            Random random = new Random();
            int randChoice = random.Next(3);
            switch (randChoice)
            {
                case 0:
                    return ("rock");
                    break;
                case 1:
                    return ("paper");
                    break;
                default:
                    return ("scissors");
                    break;


            }
        }
        //checks validity of choice (rock, paper or scissors)
        static bool isValidChoice(string choice)
        {
            choice = choice.ToLower();//make choice input lower case
            switch (choice)
            {
                case "rock":
                    return (true);
                case "paper":
                    return (true);
                case "scissors":
                    return (true);
                default:
                    return (false);
            }


        }
        //converts choice to numerical representation
        static int getChoiceNum(string choice)
        {
            choice = choice.ToLower();//make choice input lower case
            switch (choice)
            {
                case "rock":
                    return (0);
                case "paper":
                    return (1);
                default:
                    return (2);
            }
        }
    }
}
