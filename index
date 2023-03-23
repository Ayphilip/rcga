# Online Python-3 Compiler (Interpreter)
import random
import math

# define the fitness function to be optimized (Rastrigin function)
def fitness_function(x):
    n = len(x)
    A = 10
    return A * n + sum(xi ** 2 - A * math.cos(2 * math.pi * xi) for xi in x)

# define the genetic algorithm parameters
population_size = 50
mutation_rate = 0.1
mutation_range = 0.1
crossover_rate = 0.9
generations = 100

# initialize the population
population = [[random.uniform(-5.12, 5.12) for i in range(10)] for j in range(population_size)]


def roulette_wheel_selection(fitness_probabilities):
    r = random.uniform(0, 1)
    c = fitness_probabilities[0]
    i = 0
    while c < r:
        i += 1
        c += fitness_probabilities[i]
    return i

def real_crossover(parent1, parent2, crossover_rate):
    # Perform real-valued crossover using uniform crossover
    child1 = []
    child2 = []
    for i in range(len(parent1)):
        if random.random() < crossover_rate:
            alpha = random.uniform(0, 1)
            child1.append(alpha * parent1[i] + (1 - alpha) * parent2[i])
            child2.append(alpha * parent2[i] + (1 - alpha) * parent1[i])
        else:
            child1.append(parent1[i])
            child2.append(parent2[i])
    return [child1, child2]

def real_mutate(individual, mutation_rate, mutation_range):
    # Perform real-valued mutation using Gaussian mutation
    mutated_individual = []
    for i in range(len(individual)):
        if random.random() < mutation_rate:
            mutated_gene = individual[i] + random.gauss(0, mutation_range)
            mutated_gene = max(min(mutated_gene, 10), -10)  # limit the gene to [-10, 10]
            mutated_individual.append(mutated_gene)
        else:
            mutated_individual.append(individual[i])
    return mutated_individual


# evolve the population over multiple generations
for gen in range(generations):
    # evaluate the fitness of each individual
    fitness_values = [fitness_function(individual) for individual in population]
    
    # select parents using roulette wheel selection
    total_fitness = sum(fitness_values)
    fitness_probabilities = [fitness / total_fitness for fitness in fitness_values]
    parent_indices = [roulette_wheel_selection(fitness_probabilities) for i in range(population_size)]
    
    # create offspring through crossover and mutation
    offspring = []
    
    
    for i in range(0, population_size, 2):
        parent1 = population[parent_indices[i]]
        parent2 = population[parent_indices[i + 1]]
        child1, child2 = real_crossover(parent1, parent2, crossover_rate)
        child1 = real_mutate(child1, mutation_rate, mutation_range)
        child2 = real_mutate(child2, mutation_rate, mutation_range)
        offspring.extend([child1, child2])
    
    # replace the population with the offspring
    population = offspring

# select the best individual from the final population
fitness_values = [fitness_function(individual) for individual in population]
best_individual = population[fitness_values.index(min(fitness_values))]

print("Best solution:", best_individual) 
print("Fitness value:", fitness_function(best_individual))
