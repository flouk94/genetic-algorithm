# genetic-algorithm
projet IN104

import random
class Individual:
	#we define the class individual with a chromosome which is a list of element
	#and its fitness, it means is coefficient of being interessant for our problem
	def __init__(self,chromosome,fitness):
		self.chromosome = chromosome
		self.fitness = fitness

class population:
#we define the population with a list of list of element and n the number of list
	def __init__(self,n,Liste_individu):
		self.n = n
		self.Liste_individu = Liste_individu

def create_new_list(L):

# With a list L length n we create 2*n other lists
    n=len(L)
    Liste_individu=[]
    
    for i in range(2*n):
        List=[]
        
        for k in range(n):
            List.append(random.randint(0,1)) #our elements are just composed of 0 and 1
        
        Liste_individu.append(List)
    
    population.Liste_individu=Liste_individu
    #we define our new population composed of 2*n lists
    population.n=n
    
    return (population)
   
def fitness(Individual):
	#to define the fitness of a individual we define its fitness thanks to a function
	k=0.5
	chromosome=Individual.chromosome
	S=0
	lenght=0
	
#the fitness is coefficient that depends of the lenght and the sum of a chromosome
	for i in range(len(chromosome)):
		S=S+chromosome[i]*L[i]
		lenght=lenght+chromosome[i]
#we calcul S and lenght and we add a coefficient k that we can change 
#to take in count more the sum or the lenght
	Individual.fitness=k*S +(1-k)/(1+lenght)
#we return the individual with its good fitness
	return(Individual)
