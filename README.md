# genetic-algorithm
projet IN104

import random

class Individual:
	def __init__(self,chromosome,fitness):
		self.chromosome = chromosome
		self.fitness = fitness

class population:
	def __init__(self,n,Liste_individu):
		self.n = n
		self.Liste_individu = Liste_individu
