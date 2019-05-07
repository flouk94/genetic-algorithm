# genetic-algorithm
projet IN104

import random
import time

start_time = time.time()


class Individual:
	
	#the individual is defined by its chromosome (list of 0 and 1) and its fitness (a score)
	#to keep the best ones

	def __init__(self,chromosome,fitness):
		self.chromosome = chromosome
		self.fitness = fitness

class population:

#the population is a list of n individuals 
	
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
	Individual.fitness=abs(k*S**2 +(1-k)/(1+lenght))
#we return the individual with its good fitness
	return(Individual)





def crossover(Individual_A,Individual_B):
	#we define a function of crossover where 2 chromosomes will mix 
		n=len(Individual_A.chromosome)
		#we create the two new elements who will remplace the two parents in the population
		child1=[]
		child2=[]
		#we choose a number aleatory in 0:n where the mix will happen on the chromosome
		split = random.randint(0, n)
		
		child1=Individual_A.chromosome[0:split]+Individual_B.chromosome[split+1:n]
		child2=Individual_B.chromosome[0:split]+Individual_A.chromosome[split+1:n]
		#we remplace the old ones by the new ones
		
		Individual_A.chromosome=child1
		Individual_B.chromosome=child2
		#and we return the two individuals at the end of the crossover
		
		return(Individual_A,Individual_B)




def mutate_individual(individual):
 # We implement the function for a mutation in a chromosome	

	n=len(individual.chromosome) #lenght chromosome

# each element of a chromosome can randomly mutate
	for idx in range (n):

		if random.uniform(0.0, 1.0) <= (1/n): #1/n is the probability to have a change of each element

				individual.chromosome = individual.chromosome[0:idx] + [1-(individual.chromosome[idx])] + individual.chromosome[idx+1:n] 
				#0 replaced by 1 and 1 replaced by 0
	#we return the new individual with his mutations
	return (individual)  





def test_sum( population ):

#we define a function test to test if in the population we have a candidate to solve our problem
#and if we have two possible candidates with a sum=0 we compare their length and we keep the one
#with the biggest lenght	

    max=0
    i=0
    l=0
    n=len(population.Liste_individu[0])
    Sol_possible=[]
    q=population.n
    S=0
    
    for k in range(q):
        for p in range(n):
            S=S+(population.Liste_individu[k][p])*L[p]
            if S==0:
                Sol_possible.append(population.Liste_individu[k])
                l=l+1
         #if the sum=0 this is a possible candidate, now we compare
#him to the other by the length  
            
                if sum(population.Liste_individu[k])>=max:
                    max=sum(population.Liste_individu[k])
                i=l
            S=0
    if i==0:
    	return([0]*n)
#we return the best candidate in the population that we have
    return(Sol_possible[i-1])






def selection(population):
#the function selection will take in argument a population and will choose individu that we will keep
#for the next generation, we will keep the individu with the highest fitness
    n=len(population.Liste_individu)
    List_fit=[0]*n
    
    for i in range(n):
        
        IndividualY=Individual(population.Liste_individu[i],fitness)
        IndividualY=fitness(IndividualY)
        List_fit[i]=IndividualY.fitness
        #we put in a list all the coefficient fitness of a list of individu

    m=0
    List_new_individu=[]
    
    while m<(n/10):
    #now we choose only one quart of this population, the ones with a great fitness
    #and we put the elements in an other list of individu	
    	idx=List_fit.index(min(List_fit))
    	List_new_individu.append(population.Liste_individu[idx])

    	del(List_fit[idx])
    #we delete the max of the list and we do it again
    	m=m+1
    
    population.Liste_individu=List_new_individu
    population.n=len(List_new_individu)


    return(population)
    
    
    
    
    
#SOLUTION=test_Somme(population)


def algo_genetic(population):
    n=len(population.Liste_individu)
#    SOLUTION=test_Somme(population)
    d=int(10*n)
    f=int(5*n)
    
    for i in range(d):
        #we do mutations for d individuals
        a=random.randint(0,n-1)
        #on choose some individuals ramdomly in the population
        IndividualX=Individual(population.Liste_individu[a],fitness)
        IndividualX=mutate_individual(IndividualX)
        population.Liste_individu[a]=IndividualX.chromosome
    
    for k in range(f):
        #we do f crossover for a population for random individual
        a=random.randint(0,n-1)
        b=random.randint(0,n-1)
        IndividualA=Individual(population.Liste_individu[a],fitness)
        IndividualB=Individual(population.Liste_individu[b],fitness)
        
        (IndividualA,IndividualB)=crossover(IndividualA,IndividualB)
        
    List_fit=[0]*n
    #we clacluate the fitness for each individual of our population
    for i in range(n):
        IndividualY=Individual(population.Liste_individu[i],fitness)
        IndividualY=fitness(IndividualY)
        List_fit[i]=IndividualY.fitness
    
    population=selection(population)
    #we selection the individu of the population that we like
    
    return(population)

#OUR PROGRAM has a problem with the zeros because it doesn't keep it for the final list
#so we have to add them at the end

#def zeros(L):
 ##
 #    for i in range(len(L)):
#       if L[i]==0:
#            S=S+1
 #   return(S)


def solution(L):
    
    population=create_new_list(L)
    S=test_sum(population)
 #we create an initial population and we test it at the begining    
    for k in range(10000):
    
    #we will do 10000 algo_gentic to change our population and we test it at the end of each one    
        population=algo_genetic(population)
        A=test_sum(population)
        #if we found a better solution we replace it
        if sum(A)>sum(S):
            S=A
    
    n=len(S)
    
    for i in range(n):

    	#then when we have found our best solution we multpliate each 0and 1 of our solution with the list L
        
        S[i]=S[i]*L[i]
    
    return(S)

def afficher_correctly(L):
    T=solution(L)
    LI=[]
    
    # to show correctly our solution we delete the zeros that are useless but we keep the zeros of the list L
    for k in range(len(T)):
       
        if T[k]!=0:
            
            LI.append(T[k])
        
        if T[k]==0 and L[k]==0:
            
            LI.append(T[k])
    
    n=len(LI)
    #we return the final result and its lenght
    print("les solutions sont:")
    return(LI,n)


L = [random.randrange(-100000, 100000) for i in range(5000)]

print(afficher_correctly(L))
print("Temps d execution : %s secondes ---" % (time.time() - start_time))



def ameliorate_moyenne(L,nb):
	S=0
	A=[]
	for k in range(nb):
		(A,a)=afficher_correctly(L)
		S=S+a
	S=S/nb
	return(S)
