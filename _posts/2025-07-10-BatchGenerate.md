---
title: BatchGenerate
description: >-
  An introduction to the functions in /BatchGenerate
authors: [pengxin, xin]
date: 2025-07-10 22:56:00 +0800
categories: [Tutorials, BatchGenerate]
tags: [BatchGenerate]
---

## CheckStructures

(

`batch_structures`: `<class 'BM4Ckit.BatchStructures.BatchStructuresBase.BatchStructures'>`

)



    

## check_distance

(

`radius_threshold`: `<class 'float'> = 1`

)


        check atomic pairwise distances that are too close (less than given `radius_threshold`)
        Args:
            radius_threshold: float, the threshold radius.
        Returns:
            mask_array: ndarray[(n_batch, ), bool], where False for failed to the check.
        

## check_surf_smoothness

(

`smoothness_threshold`: `<class 'float'> = 0.5`

`r_cutoff`: `<class 'float'> = 3.0`

`surf_check_method`: `Optional[Literal['ConnectedGraph', 'C', 'MinDistance', 'M']] = MinDistance`

)


        check whether the surface smooth enough (whether the max difference among surface atoms along z axis < `smoothness_threshold`)
        Args:
            smoothness_threshold: smoothness threshold.
            r_cutoff: the cut-off distance to form the graph or inter-atomic distance checking.
            surf_check_method: method of surface checking.
                None: no check will applied;
                'ConnectedGraph' or 'C': it will check whether the surface atoms form only one connected graph. If not, mask returns False.
                'MinDistance' or 'M': it will check for atoms whose shortest distance from other atoms exceeds the cut-off distance.

        Returns:
            mask_array: ndarray[(n_batch, ), bool], where False for failed to the check.
        

## InitAdsStructure

(

`slabs`: `<class 'BM4Ckit.BatchStructures.BatchStructuresBase.BatchStructures'>`

`ads`: `<class 'torch.Tensor'>`

`ads_elements`: `Dict`

`vaccuum_direction`: `Literal['x', 'y', 'z'] = z`

`device`: `str | torch.device = cpu`

`verbose`: `<class 'int'> = 0`

)

None

## run

(

`slab_site`: `List[List[int]]`

`ads_site`: `List[int]`

`bond_length`: `<class 'float'>`

`bond_coeff`: `<class 'float'> = 5.0`

`non_bond_coeff`: `<class 'float'> = 3.0`

`keep_ads_conf_coeff`: `<class 'float'> = 2.0`

)



        Args:
            slab_site: The indices of adsorption site in slabs.
            ads_site: The indices of adsorption site in adsorbate.
            bond_length: The target bond length of adsorbate and slabs.
            bond_coeff: Strength coefficient of ads-slab bond.
            non_bond_coeff: Strength coefficient of repulsiveness of non-bond atom between ads. and slab.
            keep_ads_conf_coeff: Strength coefficient of keeping original adsorbate configuration.

        Returns:
            BatchStructures: the batch structures of slabs with ads.

        

## RandReplace

(

`size`: `<class 'int'> = 1`

`seed`: `<class 'int'> = None`

`device`: `str | torch.device = cpu`

`verbose`: `<class 'int'> = 2`

)




    

## run

(

`X`: `<class 'torch.Tensor'>`

`Element_list`: `Union[List[List[str]], List[List[int]]]`

`replace_element_range`: `Dict[str | int, Tuple[str | int]]`

`replace_numbers`: `Sequence[int]`

`batch_indices`: `Union[Sequence[int], torch.Tensor, numpy.ndarray, NoneType] = None`

)



        Args:
            X: Tensor[n_batch, n_atom, 3], the atom coordinates.
            Element_list: List[List[str | int]], the atomic type (element) corresponding to each row of each batch in X.
            replace_element_range: dict((symbol of element to be replaced | index of atom in X) to be replaced : tuple(symbol | atomic number of elements to replace))
            replace_numbers: the number of times that each atom is replaced. It must have the same length of `replace_element_range`.
            batch_indices: Sequence | th.Tensor | np.ndarray | None, the split points for given X, Element_list & V_init, must be 1D integer array_like.
                the format of batch_indices is same as `split_size_or_sections` in torch.split:
                batch_indices = (n1, n2, ..., nN) will split X, Element_list & V_init into N parts, and ith parts has ni atoms. sum(n1, ..., nN) = X.shape[1]

        Returns:
