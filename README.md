# Capstone-Project
import codecademylib
import pandas as pd
import matplotlib as plt

#Task 1
species = pd.read_csv('species_info.csv')
print(species.head())

#Task 2
species_count = species.scientific_name.nunique()
species_type = species.category.unique()
conservation_statuses = species.conservation_status.unique()

#Task 3
conservation_counts = species.groupby('conservation_status').scientific_name.nunique().reset_index()
print(conservation_counts)

#Task 4
species.fillna('No Intervention', inplace = True)
conservation_counts_fixed = species.groupby('conservation_status').scientific_name.nunique().reset_index()
print(conservation_counts_fixed)

#Task 5
protection_counts = species.groupby('conservation_status')\
    .scientific_name.nunique().reset_index()\
    .sort_values(by='scientific_name')
plt.figure(figsize=(10, 4))
ax = plt.subplot()
plt.bar(range(len(protection_counts)),protection_counts.scientific_name.values)
ax.set_xticks(range(len(protection_counts)))
ax.set_xticklabels(protection_counts.conservation_status.values)
plt.ylabel('Number of Species')
plt.title('Conservation Status by Species')
plt.show()

#Task6
category_counts = species.groupby(['category', 'is_protected']).scientific_name.nunique().reset_index()
print(category_counts.head())
category_pivot = category_counts.pivot(columns='is_protected', index='category', values='scientific_name').reset_index()
print(category_pivot)

#Task7
category_pivot.columns = ['category','not_protected', 'protected']
category_pivot['percent_protected'] = category_pivot.protected/(category_pivot.protected + category_pivot.not_protected)
print(category_pivot)

#Task8
contingency = [[30, 146], [75, 413]]
from scipy.stats import chi2_contingency
chi2, pval, dof, expected = chi2_contingency(contingency)
print pval
contingency_reptile = [[30, 146], [5, 73]]
chi2, pval_reptile_mammal, dof, expected = chi2_contingency(contingency_reptile)
print pval_reptile_mammal

#Task9 - Final Thoughts on species_info.csv

#Task10
import codecademylib
import pandas as pd
import matplotlib as plt
observations = pd.read_csv('observations.csv')
print(species.head())

#Task11
species['is_sheep'] = species.common_names.apply(lambda x: 'Sheep' in x)
species_is_sheep = species[species.is_sheep]
print(species_is_sheep.head())
sheep_species = species[(species.is_sheep) & (species.category == 'Mammal')]
print(sheep_species)

#Task12
sheep_observations = pd.merge(sheep_species, observations)
print(sheep_observations.head())
obs_by_park = sheep_observations.groupby('park_name').observations.sum().reset_index()
print(obs_by_park)

#Task13
plt.figure(figsize=(16, 4))
ax = plt.subplot()
plt.bar(range(len(obs_by_park)),obs_by_park.observations.values)
ax.set_xticks(range(len(obs_by_park)))
ax.set_xticklabels(obs_by_park.park_name.values)
plt.ylabel('Number of Observations')
plt.title('Observations of Sheep per Week')
plt.show()

#Task14
baseline = 15
minimum_detectable_effect = 100*5./15
sample_size_per_variant = 870
yellowstone_weeks_observing = sample_size_per_variant/507.
bryce_weeks_observing = sample_size_per_variant/250.

#Task15 - Foot and Mouth Reduction Effort Final Thoughts
