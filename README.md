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
