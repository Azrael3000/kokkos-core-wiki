# `Kokkos::atomic_[op]`

Header File: `Kokkos_Core.hpp`

Usage:
  ```c++
  old_value =  atomic_op(ptr_to_value,update_value);
  ```

Atomicly updates the variable at the address given by `ptr_to_value` with `update_value` according to the relevant operation, 
and returns the updated value found at that address..

## Synopsis

```c++
  template<class T>
  T atomic_add_fetch(T* const ptr_to_value, const T value);

  template<class T>
  T atomic_and_fetch(T* const ptr_to_value, const T value);

  template<class T>
  T atomic_div_fetch(T* const ptr_to_value, const T value);

  template<class T>
  T atomic_lshift_fetch(T* const ptr_to_value, const unsigned shift);

  template<class T>
  T atomic_mod_fetch(T* const ptr_to_value, const T value);

  template<class T>
  T atomic_mul_fetch(T* const ptr_to_value, const T value);

  template<class T>
  T atomic_or_fetch(T* const ptr_to_value, const T value);
  
  template<class T>
  T atomic_rshift_fetch(T* const ptr_to_value, const unsigned shift);

  template<class T>
  T atomic_sub_fetch(T* const ptr_to_value, const T value);
  
  template<class T>
  T atomic_xor_fetch(T* const ptr_to_value, const T value);
```

## Description

* ```c++
  template<class T>
  T atomic_add_fetch(T* const ptr_to_value, const T value);
  ```

  Atomicly executes ` *ptr_to_value += value; return *ptr_to_value;`. 
  * `ptr_to_value`: address of the to be updated value.
  * `value`: value to be added.

* ```c++
  template<class T>
  T atomic_and_fetch(T* const ptr_to_value, const T value);
  ```

  Atomicly executes ` *ptr_to_value &= value; return *ptr_to_value;`. 
  * `ptr_to_value`: address of the to be updated value.
  * `value`: value with which to combine the original value. 

* ```c++
  template<class T>
  T atomic_div_fetch(T* const ptr_to_value, const T value);
  ```

  Atomicly executes ` *ptr_to_value /= value; return *ptr_to_value;`. 
  * `ptr_to_value`: address of the to be updated value.
  * `value`: value by which to divide the original value.. 

* ```c++
  template<class T>
  T atomic_lshift_fetch(T* const ptr_to_value, const unsigned shift);
  ```

  Atomicly executes ` *ptr_to_value << shift; return *ptr_to_value;`. 
  * `ptr_to_value`: address of the to be updated value.
  * `shift`: value by which to shift the original variable.

* ```c++
  template<class T>
  T atomic_mul_fetch(T* const ptr_to_value, const T value);
  ```

  Atomicly executes ` *ptr_to_value *= value; return *ptr_to_value;`. 
  * `ptr_to_value`: address of the to be updated value.
  * `value`: value by which to multiply the original value. 

* ```c++
  template<class T>
  T atomic_mod_fetch(T* const ptr_to_value, const T value);
  ```

  Atomicly executes ` *ptr_to_value %= value; return *ptr_to_value;`. 
  * `ptr_to_value`: address of the to be updated value.
  * `value`: value with which to combine the original value. 

* ```c++
  template<class T>
  T atomic_or_fetch(T* const ptr_to_value, const T value);
  ```

  Atomicly executes ` *ptr_to_value |= value; return *ptr_to_value;`. 
  * `ptr_to_value`: address of the to be updated value.
  * `value`: value with which to combine the original value. 

* ```c++
  template<class T>
  T atomic_rshift_fetch(T* const ptr_to_value, const unsigned shift);
  ```

  Atomicly executes ` *ptr_to_value >> shift; return *ptr_to_value;`. 
  * `ptr_to_value`: address of the to be updated value.
  * `shift`: value by which to shift the original variable.

* ```c++
  template<class T>
  T atomic_sub_fetch(T* const ptr_to_value, const T value);
  ```

  Atomicly executes `*ptr_to_value -= value`. 
  * `ptr_to_value`: address of the to be updated value.
  * `value`: value to be substracted.. 

* ```c++
  template<class T>
  T atomic_xor_fetch(T* const ptr_to_value, const T value);
  ```

  Atomicly executes ` *ptr_to_value ^= value; return *ptr_to_value;`. 
  * `ptr_to_value`: address of the to be updated value.
  * `value`: value with which to combine the original value. 

