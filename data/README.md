## Step 1: Download dataset

```bash
mkdir -p ./datasets
cd datasets
wget http://bioinf.jku.at/research/lsc/chembl20/dataPythonReduced.zip
unzip dataPythonReduced.zip
cd dataPythonReduced
wget http://bioinf.jku.at/research/lsc/chembl20/dataPythonReduced/chembl20Smiles.pckl
wget http://bioinf.jku.at/research/lsc/chembl20/dataPythonReduced/chembl20LSTM.pckl
cd ..
rm dataPythonReduced.zip
mkdir -p chembl_raw/raw
mv dataPythonReduced/* chembl_raw/raw
wget 'https://www.dropbox.com/s/vi084g0ol06wzkt/mol_cluster.csv?dl=1'
mv 'mol_cluster.csv?dl=1' chembl_raw/raw/mol_cluster.csv
```

## Step 2: The transformation process of the ChEMBL dataset
+ Remove entries with missing data (None values).
+ Exclude molecules with two or fewer non-hydrogen atoms.
+ For compounds with multiple components, keep only the largest molecule.
+ Filter out molecules outside the desired molecular weight range (below 50 or above 900).

## Step 3: Map ChEMBL IDs to STRING IDs, facilitating a bridge between ChEMBL's biochemical data and STRING's protein interaction data.
+ Map Targets to Indices: Create a list from target annotation indices and write a mapping of each target to a corresponding index into a new file. This step organizes the data for easy reference.
+ Verify SMILES Strings: Open a file containing SMILES strings and another with molecular representations. By iterating over these, the script checks that each SMILES string correctly matches its molecular structure as represented by RDKit objects, ensuring the data's accuracy and consistency.

## Step 4: Simplifies the ChEMBL dataset
+ Create Connected Subsets: Generate ChEMBL-Dense-{10, 50, 100} datasets based on connectivity.
+ Filtering: Keep only well-connected drug and assay tasks.
+ Resulting Datasets: Obtain three refined datasets with specific connectivity levels.

