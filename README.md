import random

def simulate_genetics():
    # Setup initial population: All start as 'Ll'
    # Change population_size to match your class size
    population_size = 20 
    population = [['L', 'l'] for _ in range(population_size)]
    
    # Store history for the table
    history = {i: [ "Ll" ] for i in range(population_size)}

    generations = 5

    for gen in range(generations):
        new_population = []
        
        # Shuffle to choose partners at random
        random.shuffle(population)
        
        # Pair participants (0 with 1, 2 with 3, etc.)
        for i in range(0, population_size, 2):
            parent1 = population[i]
            parent2 = population[i+1]
            
            # Produce two offspring to maintain population size
            for _ in range(2):
                viable = False
                while not viable:
                    # c. Each participant turns over top card (random allele)
                    allele1 = random.choice(parent1)
                    allele2 = random.choice(parent2)
                    offspring = sorted([allele1, allele2]) # Sorts to 'Ll' or 'LL' or 'll'
                    
                    # d. Selection pressure: 'll' cannot contribute to next gen
                    if offspring != ['l', 'l']:
                        new_population.append(offspring)
                        viable = True
                    # If 'll', the loop continues (try again)

        population = new_population
        
        # e. Record new genotypes
        for idx, genotype in enumerate(population):
            gt_str = "".join(genotype)
            history[idx].append(gt_str)

    # Print results in a format for Student Answer Packet 1
    print(f"{'Student ID':<12} | {'Gen 0':<6} | {'Gen 1':<6} | {'Gen 2':<6} | {'Gen 3':<6} | {'Gen 4':<6} | {'Gen 5':<6}")
    print("-" * 65)
    for student_id, genotypes in history.items():
        row = " | ".join(f"{gt:<6}" for gt in genotypes)
        print(f"Student {student_id+1:<3} | {row}")

if __name__ == "__main__":
    simulate_genetics()
