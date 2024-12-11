await rdkit.load();

const smiles = get('smiles');
if (!smiles) return;

console.log(smiles)
console.time('rdkit');
const mol = rdkit.Molecule.smilesToMol(smiles);

mol.addHs();
mol.EmbedMolecule();
mol.MMFFoptimizeMolecule();

const mol3d = mol.molToMolfile();
mol.delete();
console.timeEnd('rdkit');

API.createData('mol3d', mol3d);
