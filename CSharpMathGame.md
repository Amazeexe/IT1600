# Math Game
- Simple C# Math Game
- Coded for IT 2040 Challenge


```C#
using System.Reflection.Metadata;
using System.Security.Cryptography.X509Certificates;

namespace Math_Game;

//Math game project
//Welcome the user to the game
//ask user for name; if user does not enter name ask them to input again
//have user choose desired difficulty for math game 1,2,3
    // do not allow user to input invalid difficulty, ask them to input again
//set a limit on questions
    //ask user how many questions they would like: valid 3-10
        //if they input invalid number, give error message, tell them to input again
//ask the math questions
//problem format = x + y
//generate the number of math probelms specified by user
    //level 1 : single digit numbers
    //level 2 : double digit numbers
    //level 3: triple digit numbers
//get user's answer
//determine if user answer is correct
    //if correct: YaY! You Got It Right, move on to next problem,
    //if incorrect: OOPS! You Got It WRONG!!
    //user can only have 3 attempts per problem
    //if user does not give correct answer after 3 attempts output answer
    //move to next problem
//calculate final score, congratulate user on effort
//display correct percentage to two decimal places
//must have at least 4 functions
class Program
{
    static void Main(string[] args)
    {
        string userName = GetUserName();
        int difficulty = GetDifficultyLevel();
        int questionLimit = GetQuestionLimit();
        PlayGame(userName, difficulty, questionLimit );
    }

    //get username function
    //have user input name
    //trim user input
    //if no user input require them to enter name again

    static string GetUserName()
    {
        string name;
        do
        {
            Console.WriteLine("Please enter your name:");
            name = Console.ReadLine().Trim();
            if (string.IsNullOrEmpty(name))
            {
                Console.WriteLine("Please enter a valid name.");
            }

        } while (string.IsNullOrEmpty(name));
        return name;
    }


    //function to get difficulty level
    //difficulty level 1-3
    //if user input isnt valid prompt them to input again

    static int GetDifficultyLevel()
    {
        int level;
        do
        {
            Console.WriteLine("Please select a difficulty level (1: Easy, 2: Medium, 3: Hard)");
            string input = Console.ReadLine();
            if (int.TryParse(input , out level) && level >=1 && level <= 3)
            {
                return level;
            }
            Console.WriteLine("Invalid option. Please choose 1, 2, or 3.");

        }while (true);
    }

    //function to get question limit
    //prompt user to input question limit
    //parse user input
    //user input question limit: valid limit 3-10
    //if user inputs invalid question limit prompt them to try again

    static int GetQuestionLimit()
    {
        int limit;
        do
        {
            Console.WriteLine("How many problems would you like to attempt?");
            string input = Console.ReadLine();
            if (int.TryParse(input, out limit) && limit >= 3 && limit <=10)
            {
                return limit;
            }
            Console.WriteLine("Invalid number. Please enter a number between 3 and 10!");
        } while (true);
    }



    //function to play the game
    // question format x + y =
    // single, double, triple digits according to difficulty level
    //randomly generate problems using random

    static void PlayGame(string userName, int difficulty, int questionLimit)
    {
        //var to store correct answers, start at 0
        int correctAnswers = 0;
        Random rand = new Random();
        
        for (int i = 0; i < questionLimit; i++)
        {
            int x = GenerateRandomNumber(difficulty, rand);
            int y = GenerateRandomNumber(difficulty, rand);
            int correctAnswer = x + y;

            //output random math question
            Console.WriteLine($"Question {i + 1}: {x} + {y} = ?");
            if (AskQuestion(correctAnswer))
            {
                Console.WriteLine("YaY! You Got It Right!!!");
                correctAnswers++;
            }
            else
            {
                Console.WriteLine($"OOPS! You Got it WRONG!!! The correct answer was {correctAnswer}.");
            }
        }

        Console.WriteLine($"Congratulations, {userName}! You answered {correctAnswers} out of {questionLimit} questions correctly.");
        double scorePercentage = (double)correctAnswers / questionLimit * 100;
        Console.WriteLine($"Your score: {scorePercentage:F2}%");

    }

    //random number function
    //switch case to select difficulty
        //case 1, single digit 1-10
        //case 2, double digit 10-100
        //case 3, triple digit 100-1000
    static int GenerateRandomNumber(int difficulty, Random rand)
    {
        switch (difficulty)
        {
            case 1:
                return rand.Next(1, 10);
            case 2:
                return rand.Next(10, 100);
            case 3:
                return rand.Next(100, 1000);
            default:
                return 0;

        }
    }

    //function to ask questions
    //max of 3 attempts
    //display correct answer after 3rd attempt
    static bool AskQuestion(int correctAnswer)
    {
        for (int attempts = 0; attempts < 3; attempts++)
        {
            Console.WriteLine("Your answer: ");
            string input = Console.ReadLine();
            if (int.TryParse(input, out int userAnswer))
            {
                if (userAnswer == correctAnswer)
                {
                    return true;
                }
            }
            Console.WriteLine("Incorrect answer. Please try again.");

        }
        return false;
    }

}
```
## [Back to Home](README.md)

## [Visit My PC Specs](MyList.md)
