---
title: load_files
description: >-
  An introduction to the functions in /Preprocessing/load_files.py
authors: [pengxin, xin]
date: 2025-07-08 15:53:00 +0800
categories: [Tutorials, Preprocessing]
tags: [Preprocessing, load_files]
---

**Please note that all methods in *load_files.py* inherits *[BatchStructuresBase.py](https://hectopasca1.github.io/BM4Ckit_wiki/posts/BatchStructuresBase/)*.**

## POSCARs2Feat

(

`path`: `<class 'str'> = ./`

`verbose`: `<class 'int'> = 0`

`args`: `<class 'inspect._empty'>`

`kwargs`: `<class 'inspect._empty'>`

)


    Read and convert a folder of POSCAR files from given path into arrays of atoms, coordinates, cell vectors, etc.
    

## read

(

`file_list`: `Optional[List] = None`

`output_coord_type`: `<class 'str'> = cartesian`

)



        Args:
            file_list: list (or other Sequences), the list of selected files to be read. 'None' means read all files in the input path.
            output_coord_type: str, 'cartesian' or 'direct'. The coordination type of output atom coordination.

        Returns:

        

## OUTCAR2Feat

(

`path`: `<class 'str'>`

`verbose`: `<class 'int'> = 1`

)


    Read atoms, coordinates, atom numbers, energies and force in OUTCARs from given path.
    Notes: Because OUTCAR does not store any information of fixed atom (selective dynamics), all atoms would be set to FREE!!

    Parameters:
        path: str, the path of batched OUTCAR-like files. The Sample ids would be labeled as its file names.
    

## read

(

`file_list`: `Optional[List[str]] = None`

`n_core`: `<class 'int'> = -1`

`backend`: `<class 'str'> = loky`

)


        Parameters:
            file_list: List[str], the list of files to read. Default for all files under given path.
            n_core: int, the number of CPU cores used in reading files.
            backend: backend for parallelization in joblib. Options: 'loky', 'threading', 'multiprocessing'.

        Return: None
        Update the attribute self.data.
        

## ASETraj2Feat

(

`path`: `<class 'str'>`

`verbose`: `<class 'int'> = 1`

)


    read ASE files to BatchStructures.
    

## read

(

`file_list`: `<class 'inspect._empty'> = None`

`n_core`: `<class 'int'> = -1`

`backend`: `Union[Literal['loky', 'threading', 'multiprocessing'], str] = loky`

)



## ExtXyz2Feat

(

`path`: `<class 'str'>`

`verbose`: `<class 'int'> = 1`

)


    Read extxyz file with multiple structures.
    

## read

(

`file_list`: `<class 'inspect._empty'> = None`

`n_core`: `<class 'int'> = -1`

`backend`: `Union[Literal['loky', 'threading', 'multiprocessing'], str] = loky`

`lattice_tag`: `<class 'str'> = lattice`

`energy_tag`: `<class 'str'> = energy`

`column_info_tag`: `<class 'str'> = properties`

`element_tag`: `<class 'str'> = species`

`coordinates_tag`: `<class 'str'> = pos`

`forces_tag`: `str | None = forces`

`fixed_atom_tag`: `str | None = move_mask`

)


        Read *.extxyz files to BatchStructures.
        Args:
            file_list: List[str], the list of files to read. Default for all files under given path.
            n_core: int, the number of CPU cores used in reading files. -1 for all cores.
            backend: backend of parallel reading in `joblib`.
            lattice_tag: key-words of lattice information in *.extxyz file, at each structure's 2nd line.
            energy_tag: key-words of structure's energy in *.extxyz file.
            column_info_tag: key-words of column content information in *.extxyz file. The column content has such format:
                             `content 1`:`data type 1`:`column occupied number 1`:`content 2`:`data type 2`:`column occupied number 2`: ...
                             detailed see https://wiki.fysik.dtu.dk/ase/dev/_modules/ase/io/extxyz.html.
            element_tag: As a content in `column_info_tag`, name of element column.
            coordinates_tag: As a content in `column_info_tag`, name of atom coordinates column.
            forces_tag: As a content in `column_info_tag`, name of forces column. If the file does not contain forces, set it to None.
            fixed_atom_tag: As a content in `column_info_tag`, name of the mask column specified which atom was fixed.

        Returns: None
        All data would update as class attributes.
        

## load_from_csv

(

`file_name`: `<class 'str'>`

`label_type`: `<class 'type'> = <class 'float'>`

`ignore_None_label_samp`: `<class 'bool'> = True`

`read_column`: `Tuple[int, int] = (0, 1)`

`has_title_line`: `<class 'bool'> = False`

)


    load information of a csv file into a dict of {samp_1:label_1, ...}.

    Parameters:
        file_name: str, csv file of 2 columns (sample name, sample label)
        label_type: type, type of sample label
        ignore_None_label_samp: bool, whether ignore None label samples i.e., not put them into output dict
        read_column: Tuple[int,int], the 2 columns to read, where the 1st column as keys and the 2nd as values.
        has_title_line: bool, whether ignore the 1st line which is the title or descriptions.

    Return:
        dict of {samp_1:label_1, ...} | dict, id_list of [samp_names]
    

## Cif2Feat

(

`path`: `<class 'str'>`

`verbose`: `<class 'int'> = 1`

)


    Read CIF file with multiple structures.
    Notes: CIF file could not contain the fixation information, so all atoms would be free.

    

## read

(

`file_list`: `<class 'inspect._empty'> = None`

`n_core`: `<class 'int'> = -1`

`backend`: `Union[Literal['loky', 'threading', 'multiprocessing'], str] = loky`

)



## load_from_structures

(

`path`: `<class 'str'>`

)


    Load BatchStructure memory-mapping files from `path` and return this BatchStructures.
    Args:
        path: the path of BatchStructure memory-mapping files.

    Returns: BatchStructures with read data.

    

## Output2Feat

(

`path`: `<class 'str'>`

`verbose`: `<class 'int'> = 1`

)


    A class of post-processing to reading output files of BatchOptimization and BatchMD
    

## read

(

`file_list`: `List[str]`

`n_core`: `<class 'int'> = -1`

`backend`: `<class 'inspect._empty'> = loky`

)
