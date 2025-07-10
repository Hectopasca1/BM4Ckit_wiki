---
title: DataLoaders
description: >-
  An introduction to the functions in /TrainingMethod/DataLoaders.py
authors: [pengxin, xin]
date: 2025-07-10 16:45:00 +0800
categories: [Tutorials, TrainingMethod]
tags: [TrainingMethod, DataLoaders]
---

## DglGraphLoader

(

`data`: `Dict[Union[Literal['data', 'labels'], Literal['data', 'names']], Any]`

`batch_size`: `<class 'int'>`

`device`: `str | torch.device = cpu`

`shuffle`: `<class 'bool'> = True`

`is_train`: `<class 'bool'> = True`

`data_names`: `Optional[Sequence[str]] = None`

)


    A Data loader to form dgl graph IN MEMORY

    Args:
        data:
            when is_train == True:
                Dict: {
                    'data': List[dgl.Graph],
                    'label': Dict{'energy': Sequence[float], 'forces': Sequence[np.NDArray[n_atom, 3]]}
                }. Wherein 'force' is optional.
            else see `data_names`.
        batch_size: batch size.
        device: the device that data put on.
        shuffle: whether shuffle data.
        is_train: if `is_train` = True, data need to contain labels; else data need not contain labels and the return of labels [i.e., next(iter(dataloader))] was depended on `contain_names`.
        data_names: only works when `is_train` = False.
                if `data_names` is not None, it should be a Sequence(data names) with the same order as data,
                and the returned `labels` [i.e., next(iter(dataloader))] would be data_names instead of "energy" or "forces",
                else `labels` would be None.

    Yields:
            (dgl.DGLGraph, {'energy': energy, 'forces': force})
         or (dgl.DGLGraph, {'energy': energy, })
         or (dgl.DGLGraph, data_names | None) [when is_train == False]

    

## shuffle

(

)



## PyGDataLoader

(

`data`: `Dict[Union[Literal['data', 'labels'], Literal['data', 'names']], Any]`

`batch_size`: `<class 'int'>`

`device`: `str | torch.device = cpu`

`shuffle`: `<class 'bool'> = True`

`is_train`: `<class 'bool'> = True`

`data_names`: `Optional[Sequence[str]] = None`

)


    A Data loader to form pygData IN MEMORY

    Args:
        data: pyg.Data that contain attributes `pos`, `cell`, `atomic_numbers`, `natoms`, `tags`, `fixed`, `pbc`, `idx`.
              `pos`: Tensor, atom coordinates.
              `cell`: Tensor, cell vectors.
              `atomic_numbers`: Tensor, atomic numbers, corresponding to `pos` one by one.
              `natoms`: int, number of atoms.
              `tags`: Tensor, to be compatible with 'FAIR-CHEM' (https://fair-chem.github.io/),
                      which fixed slab part is set to 0, free slab part is 1, adsorbate is 2.
              `fixed`: Tensor, fixed tag, which fixed atoms are 0, free atoms are 1.
              `pbc`: List[bool, bool, bool], where to be periodic at x, y, z directions.
        batch_size: batch size.
        device: the device that data put on.
        shuffle: whether shuffle data.
        is_train: if `is_train` = True, data need to contain labels; else data need not contain labels and the return of labels [i.e., next(iter(dataloader))] was depended on `contain_names`.
        data_names: only works when `is_train` = False.
                if `data_names` is not None, it should be a Sequence(data names) with the same order as data,
                and the returned `labels` [i.e., next(iter(dataloader))] would be data_names instead of "energy" or "forces",
                else `labels` would be None.

    Yields:
            (pyg.Data, {'energy': energy, 'forces': force})
         or (pyg.Data, {'energy': energy, })
         or (pyg.Data, data_names | None) [when is_train == False]

    

## shuffle

(

)
