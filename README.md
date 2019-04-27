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
