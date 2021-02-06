# DiceProbabilities.py-
#Python program that simulates a dice game with the computational technique known as Monte Carlo. Given The number of sides on each die, the number of dice, and the number of #simulations to perform, program calculates the sum of the numbers on the dice. Then, after the specified
#number of simulations. Program also produces an estimate of the probability of each possible sum. 
import random


def throwTwoDice(R):
   """
   throws two independent dice and returns the result in a 2-tuple
   """
   die1 = R.randrange(1,7)   
   die2 = R.randrange(1,7)
   return (die1, die2)
# end ThrowTwoDice()


# make main a function to eliminate global variables   
def main(SEED=None):

   numberOfTrials = 1_000_000

   # Create a random number generator
   rng = random.Random(SEED) 

   # perform simulation, record and print frequencies
   frequency = 13*[0]  # same as [0,0,0,0,0,0,0,0,0,0,0,0,0]
   for i in range(numberOfTrials):
      t = throwTwoDice(rng)
      frequency[t[0]+t[1]] += 1;
   # end for

   print()
   print("Frequencies:")
   print(frequency)


   # calculate relative frequencies, probabilities and errors
   relativeFrequency = [0, 0]
   probability = [0,0]
   error = [0,0]
   for i in range(2, len(frequency)):
      relativeFrequency.append(frequency[i]/numberOfTrials)
      probability.append(min(i-1,13-i)/36)
      error.append(abs(probability[i]-relativeFrequency[i]))
   # end for


   #print(relativeFrequency)
   #print(probability)
   #print(error)
   print()


   # print results
   f1 = "{0:<10}{1:<22}{2:<22}{3:<22}"
   f2 = 71*"-"
   f3 = "{0:>3}{1:<22.15f}{2:<22.15f}{3:<.15f}"
   print(f1.format("Sum","Relative Frequency","Probability","Error"))
   print(f2)
   for i in range(2, len(frequency)):
      print(f3.format(i, relativeFrequency[i], probability[i], error[i]))
   #end for

   print()

# end main()


if __name__=='__main__':

   main()
