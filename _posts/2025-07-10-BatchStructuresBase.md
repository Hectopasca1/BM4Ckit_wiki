---
title: BatchStructuresBase
description: >-
  An introduction to the functions in /BatchStructures/BatchStructuresBase.py
authors: [pengxin, xin]
date: 2025-07-10 01:58:00 +0800
categories: [Tutorials, BatchStructures]
tags: [BatchStructures, BatchStructuresBase]
---

## bm.Structures

(

)


    The base class of batch structures.
    

## append

(

`batch_structures`: `<class 'inspect._empty'>`

`strict`: `<class 'bool'> = True`

)


        Append information of another BatchStructures to self.
        If original data do not have some properties but appending data do,
         these properties of original data would be padded with `None`, and vice versa.
        Args:
            batch_structures: the BatchStructures to append
            strict: If True, `batch_structures` contains any id which is already in `self` would raise an Error;
                    otherwise, the data will be overwritten if encountered the same id.

        Returns: None

        

## cartesian2direct

(

)

 Convert Cartesian coordinates to Direct coordinates. Only work in 'L' Mode. 

## contain_all

(

`elements`: `Union[List[str], Set[str]]`

)


        Return a view of BatchStructures that contain all given elements.
        

## contain_any

(

`elements`: `Union[List[str], Set[str]]`

)


        Return a view of BatchStructures that contain any of given elements.
        

## contain_only_in

(

`elements`: `Union[List[str], Set[str]]`

)


        Return a view of BatchStructures that only contain given elements.
        

## direct2cartesian

(

)

 Convert Direct coordinates to Cartesian coordinates. Only work in 'L' Mode. 

## elem_distribution

(

`count_for`: `Literal['Atom', 'Structure'] = Structure`

)


        return a Dict[str, int] of {element: frequency} that shows the distribution of elements in BatchStructures.

        Parameters:
            count_for: 'Atom' or 'Structure', count element frequency by each atom in structures or each structure.
        

## extend

(

`batch_structures_list`: `Sequence`

`strict`: `<class 'bool'> = True`

)


        Extend a list of BatchStructures to self.
        If original data do not have some properties but appending data do,
         these properties of original data would be padded with `None`, and vice versa.
        Args:
            batch_structures_list: the BatchStructures to append
            strict: If True, `batch_structures` contains any id which is already in `self` would raise an Error;
                    otherwise, the data will be overwritten if encountered the same id.

        Returns: None

        

## generate_atom_list

(

`force_update`: `<class 'bool'> = False`

)


        Generate an attribute self.Atom_list (List[str]) which is the atom lists in order of the atomic coordinates sequence.

        Parameters:
            force_update: bool. if False, Atom_list would not be updated when it's not None.
        

## generate_atomic_number_list

(

`force_update`: `<class 'bool'> = False`

)


        Generate attribute self.Atomic_number_list (List[int]) which is the atomic number lists in order of the sequence of atom coordinates.

        Parameters:
            force_update: bool. if False, Atomic_number_list would not be updated when it's not None.
        

## generate_dist_mat

(

`supercell_indices`: `<class 'inspect._empty'> = [[ 0.00000000e+00  0.00000000e+00  0.00000000e+00]]`

)


        Parameters:
            supercell_indices: NDArray[n_supercell, 3], the indices of supercells that calculate distance.

        self.Dist_mat Format: List[Tensor[(n_prim_cells, n_atom, n_atom)]]
        

## load

(

`path`: `<class 'str'>`

`data_slice`: `Optional[Tuple[int, int]] = None`

`mode`: `Literal['w', 'a'] = w`

)


        Load data from saved files.
        Args:
            path: the file path.
            data_slice: The piece of data in files to be read. If None, all data in files would be read into memory.
            mode: the data load mode. 'W' for write or overwrite existing data from data in file; 'a' for appending data in file to existing data.

        Returns: None

        

## load_from_file

(

`path`: `<class 'str'>`

`data_slice`: `Optional[Tuple[int, int]] = None`

)


        The class method version for loading data from saved files.
        WARNING: It would overwrite the existing BatchStructure data. Use `self.load(..., mode='a')` to retain existing data.
        Args:
            path: the file path.
            data_slice: The piece of data in files to be read. If None, all data in files would be read into memory.

        Returns: Self with loaded data.

        

## not_contain_all

(

`elements`: `Union[List[str], Set[str]]`

)


        Return a view of BatchStructures that Not contain all given elements at the same time.
        

## not_contain_any

(

`elements`: `Union[List[str], Set[str]]`

`verbose`: `<class 'int'> = 0`

)


        Return a view of BatchStructures that Not contain any of given elements.
        

## rearrange

(

`indices`: `List[int]`

)


        Rearrange the order of samples by given indices.
        Args:
            indices: indices of sample orders.

        Returns: None

        

## remove

(

`key`: `int | str | slice`

)


        Remove the data of given `key` in-place.
        Args:
            key: int for index, str for Sample_ids, slice for a slice of indices.

        Returns: None

        

## remove_copy

(

`key`: `int | str | slice`

)


        Remove the data of given `key` in a copy of self and return. The original data is not affected.
        Args:
            key: int for index, str for Sample_ids, slice for a slice of indices.

        Returns: copy of

        

## revise

(

`index`: `int | str`

`rev_Sample_ids`: `None | str = None`

`rev_Cells`: `None | numpy.ndarray = None`

`rev_Elements`: `Optional[List[str]] = None`

`rev_Numbers`: `Optional[List[int]] = None`

`rev_Coords_type`: `Optional[Literal['C', 'D']] = None`

`rev_Coords`: `None | numpy.ndarray = None`

`rev_Fixed`: `None | numpy.ndarray = None`

`rev_Energies`: `None | float = None`

`rev_Forces`: `None | numpy.ndarray = None`

`rev_Labels`: `Any | None = None`

)


        Revising data of given `index`. None is for not changing.
        Args:
            index:
            rev_Sample_ids:
            rev_Cells:
            rev_Elements:
            rev_Numbers:
            rev_Coords_type:
            rev_Coords:
            rev_Fixed:
            rev_Energies:
            rev_Forces:
            rev_Labels:

        

## save

(

`path`: `<class 'str'>`

`mode`: `Literal['w', 'a'] = w`

)


        Saving this BatchStructures to a numpy memory-mapping file.
        Each attribute in BatchStructures will be saved in the numpy memmap file with the same name.
        Additionally, file 'head' will record the information which is data type & shape of all attributes, and record which attributes are `None`.

        Args:
            path: the saving directory.
            mode: if 'w', create or overwrite the existing file for reading and writing. If 'a', data will append to the existing file.

        Returns: None

        

## select_by_element_number

(

`element_number_range`: `Tuple[float, float]`

)


        Return a view of BatchStructures that element number between element_number_range.
        

## select_by_energies

(

`energy_range`: `Tuple[float, float]`

)


        Return a view of BatchStructures that Energies between energy_range.
        

## select_by_prop

(

`prop`: `<class 'str'>`

`prop_range`: `Tuple[float, float]`

)


        Return a view of BatchStructures that given properties of BatchStructures between prop_range.
        The given properties must be comparable.

        Args:
            prop: an attribute name of self e.g., "Number", "Energies"
            prop_range: Tuple[float, float], range of prop to select. It is a left closed right open interval.

        Returns:
            BatchStructures which is a view of self
        

## select_by_sample_id

(

`pattern`: `<class 'str'>`

)


        Return a view of BatchStructures in which sample id could match the given pattern.
        Regular expressions are supported.
        For non-string sample id, str(*) would be applied first to convert id into string.
        Args:
            pattern: the (regular expressions) pattern to match sample ids in self.

        Returns: BatchStructures

        

## set_Energies

(

`val`: `Union[Sequence, Dict]`

)


        Set or reset self.Energies from input `val`.
        Args:
            val: the input values to set self.Energies
                if Dict, val: {sample_id: energy, ...}; if Sequence, it must have the same order of self.Sample_ids.

        Returns: None

        

## set_Forces

(

`val`: `Union[Sequence[numpy.ndarray], Dict[str, numpy.ndarray]]`

)


        Set or reset self.Forces from `val`.
        Args:
            val: the input values to set self.Forces
                if Dict, val: {sample_id: forces, ...}; if Sequence, it must have the same order of self.Sample_ids.

        Returns:

        

## set_Labels

(

`val`: `Union[Sequence, Dict, numpy.ndarray]`

)


        Set or reset self.Labels from input `val`.
        Args:
            val: the input values of self.Labels to set.
            If Dict, val: {sample_id: energy, ...}; if Sequence, it must have the same order of self.Sample_ids.

        Returns: None

        

## show

(

`number`: `int | slice`

)


        Show the information of samples in given slice `number`.
        Args:
            number: the slice of samples to show.

        Returns: None.

        

## shuffle

(

`seed`: `<class 'int'> = None`

)


        Shuffle the samples with given random seed.
        Args:
            seed: random seed.

        Returns: None

        

## sort_split_by_natoms

(

`labels`: `Union[Dict, List, NoneType] = None`

`split_ratio`: `<class 'float'> = 0.2`

`n_core`: `<class 'int'> = 1`

`verbose`: `<class 'int'> = 0`

)


        Rearrange samples with different atom number into List[np.array] that list of NDArrays with the same atom number.
        Only work in 'L' Mode.

        Parameters:
            labels: Dict[id, label]|List[label]|None, the labels of samples. If labels is a List, it must have the same order as self.Sample_ids. If None, labels would be set to self.Labels.
            split_ratio: float between 0 and 1, the ratio of validation set.
            n_core:
            verbose: control the verboseness of output

        Returns:
            training_batches, val_batches: List_1[List_2[NDArray]]. List_1 is of diff. n_atom cells, List_2 is of (Cell, Atomic_number_list, Atom_coords)
            training_labels, val_labels: List[NDArray]. List is of diff. n_atom cells, NDArray is label.
            training_args, val_args: List[NDArray]. List is of diff. n_atom cells, NDArray is the indices of samples in self.Samp_id.
        

## write2text

(

`output_path`: `<class 'str'> = ./`

`indices`: `Union[int, str, List[int], Tuple[int, int], NoneType] = None`

`file_format`: `Literal['POSCAR', 'cif', 'xyz', 'xyz_forces'] = POSCAR`

`file_name_list`: `Union[str, Sequence[str], NoneType] = None`

`n_core`: `<class 'int'> = -1`

)


        Write selected structures to text files in given format.
        Args:
            indices: the selection indices of `self`. If Tuple, structures between `indices[0]` and `indices[1]` will be selected.
            file_format: the format of written files.
                'POSCAR': vasp POSCAR format
                'cif': crystallographic information file
                'xyz': ext-xyz file that only contains atomic positions
                'xyz_forces': ext-xyz file that contains atomic positions and forces
            output_path: the directory of output file.
            file_name_list: the list of file names. If None, it would be set to `Sample_ids`.
            n_core: number of CPU cores to write in parallel. `-1` for all available CPU cores.

        Returns: None
