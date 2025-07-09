---
title: preprocessing
description: >-
  An introduction to the functions in /Preprocessing/preprocessing.py
authors: [pengxin, xin]
date: 2025-07-10 01:45:15 +0800
categories: [Tutorials, Preprocessing]
tags: [Preprocessing, preprocessing]
---

## CreateASE

(

`verbose`: `<class 'int'> = 0`

)


    Create a List[ASE.Atoms] by input crystal information.

    Parameters:
        verbose: int, control the verboseness of output.

    Methods:
        create:
            parameters:
                cell_vectors: tensor with shape (batch_size, 3, 3), batch of cell vectors.
                atomic_numbers: tensor with shape (batch_size, n_atom), batch of atomic numbers in each cell.
                atomic_coordinates: tensor with shape (batch_size, n_atom, 3), batch of Cartesian coordinates x,y,z in each cell.
                supercell_index: tensor with shape (3,), the index of cell with respect to the original cell.
            return:
                List[ase.Atoms] with length batch_size
    

## array2ase

(

`symb`: `Sequence`

`pos`: `Sequence`

`cell`: `Sequence`

`pbc`: `Union[Tuple[bool, bool, bool], bool] = (True, True, True)`

`set_tags`: `<class 'bool'> = True`

`n_core`: `<class 'int'> = -1`

)


        Convert to ase.Atoms from the given Sequence of symbols, positions, cell vectors and pbc information.

        Parameters:
            n_core:
            set_tags:
            symb: Sequence[Sequence], the sequence of element lists.
            pos: Sequence[Sequence], the sequence of atom coordinates lists.
            cell: Sequence[Sequence], the sequence of cell vectors lists.
            pbc: bool|Tuple[bool, bool, bool], the direction of periodic boundary condition (x, y, z).
        
        Returns:
            Dict[ase.Atoms], the list of Atoms instances.
        

## feat2ase

(

`feat`: `<class 'BM4Ckit.BatchStructures.BatchStructuresBase.BatchStructures'>`

`set_tags`: `<class 'bool'> = True`

`n_core`: `<class 'inspect._empty'> = -1`

)


        Convert to ase.Atoms from given BatchStructures.

        Parameters:
            feat: BatchStructures.
            set_tags: bool, whether set Atoms. tags = np.ones(n_atom) automatically.
            n_core: number of CPU cores in parallel.
        
        Returns:
            List[ase.Atoms], the list of Atoms instances.
        

## feat2ase_dict

(

`feat`: `<class 'BM4Ckit.BatchStructures.BatchStructuresBase.BatchStructures'>`

`set_tags`: `<class 'bool'> = True`

`n_core`: `<class 'int'> = -1`

)


        Convert to ase.Atoms from given BatchStructures.

        Parameters:
            n_core:
            feat: BatchStructures.
            set_tags: bool, whether set Atoms.tags = np.ones(n_atom) automatically.
        
        Returns:
            Dict[samp_id:ase.Atoms], the dict of Atoms instances with keys sample id.
        

## CreatePygData

(

`verbose`: `<class 'int'> = 0`

)


    create torch-geometric.data.Data or Batch from various types.
    

## ase2data_list

(

`atom_list`: `List[ase.atoms.Atoms]`

`n_core`: `<class 'int'> = 1`

)


        Convert a list of ase.Atoms into a pyg.Batch
        

## feat2data_list

(

`feat`: `<class 'BM4Ckit.BatchStructures.BatchStructuresBase.BatchStructures'>`

`n_core`: `<class 'int'> = 1`

)


        Convert BatchStructures into a list of pyg.Data for fair-chem model
        

## single_ase2data

(

`atoms`: `<class 'ase.atoms.Atoms'>`

)

Convert a single atomic structure to a graph.

        Args:
            atoms (ase.atoms.Atoms): An ASE atoms object.

        Returns:
            data (torch_geometric.data.Data): A geometric data object with positions, atomic_numbers, tags,
            and optionally, energy, forces, distances, edges, and periodic boundary conditions.
            Optional properties can include by setting r_property=True when constructing the class.
        

## CreateDglData

(

`verbose`: `<class 'int'> = 0`

)


    create dgl.graph from various types.
    The output DGLGraph has format as follows:
        dgl.heterograph(
            {
                ('atom', 'bond', 'atom'): ([], []),
                ('cell', 'disp', 'cell'): ([], [])
            },
            num_nodes_dict={
                'atom': n_atom,
                'cell': 1
            }
        )
        data.nodes['atom'].data['pos']: (n_atom, 3), Atom positions in Cartesian coordinates.
        data.nodes['atom'].data['Z']: (n_atom, ), Atomic numbers.
        data.nodes['cell'].data['cell']: (1, 3, 3), Cell vectors.
    

## ase2graph_list

(

`atom_list`: `List[ase.atoms.Atoms]`

`n_core`: `<class 'int'> = 1`

)


        Convert a list of ase.Atoms into a list of dgl.DGLGraph
        

## feat2graph_list

(

`feat`: `<class 'BM4Ckit.BatchStructures.BatchStructuresBase.BatchStructures'>`

`n_core`: `<class 'int'> = 1`

)


        Convert BatchStructures into a list of pyg.Data for fair-chem model
        

## single_ase2graph

(

`atoms`: `<class 'ase.atoms.Atoms'>`

)


        Convert a single atomic structure to a graph.

        Args:
            atoms (ase.atoms.Atoms): An ASE atoms object.

        Returns:
            data (torch_geometric.data.Data): A geometric data object with positions, atomic_numbers, tags,
            and optionally, energy, forces, distances, edges, and periodic boundary conditions.
            Optional properties can include by setting r_property=True when constructing the class.
        

## BlockedRW

(

`file_format`: `Literal['OUTCAR', 'EXTXYZ', 'POSCAR']`

)


    Blocked read files and save to a memory-mapping file, or load the memory-mapping file and write to specific files inversely.
    Used to manage big files that memory cannot be loaded at once.
    

## load

(

`load_path`: `<class 'str'>`

`load_range`: `Optional[Tuple] = None`

`chunck_size`: `<class 'int'> = 5000`

`verbose`: `<class 'int'> = 1`

)


        Blocked load data from given BatchStructure memory-mapping path.
        Args:
            load_path: the path to load memory-mapping.
            load_range:
            chunck_size:
            verbose:

        Returns: None
        

## save

(

`files_path`: `<class 'str'>`

`file_name_list`: `Optional[List[str]] = None`

`read_configs`: `Optional[Dict] = None`

`save_path`: `<class 'str'> = ./data`

`chunk_size`: `<class 'int'> = 32`

`verbose`: `<class 'int'> = 1`

)


        Blocked reading files in `files_path`/`file_name_list` by files_reader, and save to `save_path`.
        Args:
            files_path: path of files.
            file_name_list: list of file names to read. None for all files in given `files_path`.
            read_configs: kwargs of file reader.
            save_path: the path to save memory-mapping files.
            chunk_size: Number of files (NOT Structures) read at a time.
            verbose: verboseness of printing.

        Returns: None
        

## split_dataset

(

`data`: `<class 'BM4Ckit.BatchStructures.BatchStructuresBase.BatchStructures'>`

`ratio`: `Union[float, List[float]] = 0.9`

`save_path`: `Union[str, List[str], NoneType] = None`

`shuffle`: `<class 'bool'> = False`

`seed`: `<class 'int'> = None`

)


    Splitting the data set into parts with given ratios. It would overwrite if `save_path` already exists.
    Args:
        data: data set with BatchStructure format
        ratio: splitting ratio. If only a float number was given, data would be split into 2 parts with ratio `ratio` and `1 - ratio`.
               The summation of all ratios must be 1.
        save_path: if None, List of split data would be directly returned; otherwise they will be saved as memory-mapping files in given paths.
                   The length of `save_path` must be the same as `ratio`.
        shuffle: whether to shuffle data. If not, data will be divided sequentially.
        seed: random seed for shuffle.

    Returns: List | None
