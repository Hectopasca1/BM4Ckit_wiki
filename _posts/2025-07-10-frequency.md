---
title: frequency
description: >-
  An introduction to the functions in /BatchOptim/frequency.py
authors: [pengxin, xin]
date: 2025-07-10 22:26:00 +0800
categories: [Tutorials, BatchOptim]
tags: [BatchOptim, frequency]
---

## Frequency

(

`method`: `Literal['Coord', 'Grad'] = Coord`

`block_size`: `None | int = None`

`delta`: `<class 'float'> = 0.01`

)


    Calculate normal mode frequency by finite difference method.

    Args:
        method: 'Coord' for directly calculating 2nd-order deviations, i.e., the Hessian matrix.
                'Grad' for calculating 1st-order deviations of grad to get Hessian matrix.
        block_size: block size to calculate Hessian. `block_size`*N rows would be input at once.
                    `None` for input all (3*N)**2 rows coords at once, which requires enough memory.
        delta: finite difference delta.
    

## create_hessian

(

`func`: `Callable`

`coords`: `<class 'torch.Tensor'>`

`func_args`: `Tuple = ()`

`func_kwargs`: `Optional[Dict] = None`

`save_hessian`: `<class 'bool'> = False`

`fixed_atom_tensor`: `torch.Tensor | None = None`

)


        To calculate Hessian matrix in blocks via finite difference
        Args:
            func:
            coords: (N, 3) shape Tensor
            func_args: other input arguments of `func`.
            func_kwargs: other input keyword arguments of `func`.
            save_hessian: whether save calculated hessian as an attribute.
            fixed_atom_tensor: the indices of X that fixed, i.e., not performing vibration calculation.

        Returns:

        

## hessian_by_autograd

(

`grad_func`: `<class 'inspect._empty'>`

`X`: `<class 'torch.Tensor'>`

`grad_func_args`: `Tuple = ()`

`grad_func_kwargs`: `Optional[Dict] = None`

`fixed_atom_tensor`: `torch.Tensor | None = None`

`save_hessian`: `<class 'bool'> = False`

)



## normal_mode

(

`func`: `Callable`

`coords`: `<class 'torch.Tensor'>`

`masses`: `torch.Tensor | None = None`

`func_args`: `Tuple = ()`

`func_kwargs`: `Optional[Dict] = None`

`grad_func`: `Optional[Callable] = None`

`grad_func_args`: `Tuple = ()`

`grad_func_kwargs`: `Optional[Dict] = None`

`fixed_atom_tensor`: `torch.Tensor | None = None`

`save_hessian`: `<class 'bool'> = False`

)


        Calculating the normal modes and corresponding frequencies.
        Notice: The negative frequencies are actually imaginary frequencies.
        Args:
            func: potential energy function.
            coords: atomic coordinate tensor with shape (N, 3).
            masses: atomic masses tensor with shape (N, 3) or (N, ). `None` for tensor filled with 1.
            func_args: other input arguments of `func`.
            func_kwargs: other input keyword arguments of `func`.
            grad_func: gradient function, only used for self.method = 'Grad'.
            grad_func_args: other input arguments of `grad_func`.
            grad_func_kwargs: other input keyword arguments of `grad_func`.
            fixed_atom_tensor: (N, ) or (N, 3), the indices of X that fixed, i.e., not performing vibration calculation.
                               Only the 1st dimension will be read. Fixing partial degrees of freedom for an atom is not supported.
            save_hessian: whether save calculated hessian as an attribute.

        Returns:
            normal mode frequencies: (3N, ) shape Tensor
            normal mode coordinates: (3N, N, 3) shape Tensor
