# `Kokkos::ReducerConcept`

Header File: `Kokkos_Core.hpp`

Usage: 
  ```c++
  T result;
  parallel_reduce(N,Functor,ReducerConcept<T>(result));
  ```

. 

## Synopsis 
  ```c++
  class Reducer {
    public:
      //Required for Concept
      typedef Reducer reducer;
      typedef ... value_type;
      typedef Kokkos::View<value_type, ... > result_view_type;
      
      KOKKOS_INLINE_FUNCTION
      void join(value_type& dest, const value_type& src)  const

      KOKKOS_INLINE_FUNCTION
      void join(volatile value_type& dest, const volatile value_type& src) const;

      KOKKOS_INLINE_FUNCTION
      void init( value_type& val)  const;

      KOKKOS_INLINE_FUNCTION
      value_type& reference() const;

      KOKKOS_INLINE_FUNCTION
      result_view_type view() const;

      
      //Part of Build-In reducers for Kokkos
      KOKKOS_INLINE_FUNCTION
      Reducer(value_type& value_);

      KOKKOS_INLINE_FUNCTION
      Reducer(const result_view_type& value_);
  };
  ```

## Public Class Members

### Typedefs
   
 * `reducer`: The self type.
 * `value_type`: The reduction scalar type.
 * `result_view_type`: A `Kokkos::View` referencing where the reduction result should be placed. Can be an unmanaged view of a scalar or complex datatype (class or struct).  Unmanaged views must specify the same memory space where the referenced scalar (or complex datatype) resides.
### Constructors
 
 Constructors are not part of the concept. A custom reducer can have complex custom constructors. All Build-In reducers in Kokkos have the following two constructors:
 * ```c++
   Reducer(value_type& result)
   ```
   Constructs a reducer which references a local variable as its result location.  
 
 * ```c++
   Reducer(const result_view_type result)`
   ```
   Constructs a reducer which references a specific view as its result location.

### Functions

 * ```c++
   void join(value_type& dest, const value_type& src)  const;`
   ```
   Combine `src` into `dest`. For example, `Add` performs `dest+=src;`. 

 * ```c++
   void join(volatile value_type& dest, const volatile value_type& src) const;
   ```
   Combine `src` into `dest`. For example, `Add` performs `dest+=src;`. 

 * ```c++
   void init( value_type& val)  const;
   ```
   Initialize `val` with appropriate initial value. For example, 'Add' assigns `val = 0;`, but Prod assigns `val = 1;`   

 * ```c++
   value_type& reference() const;
   ```
   Returns a reference to the result place.

 * ```c++
   result_view_type view() const;
   ```
   Returns a view of the result place. 

### Built-In Reducers
Kokkos provides a number of built-in reducers that automatically work with the intrinsic C++ types as well as Kokkos::complex.  In order to use a Built-in reducer with a custom type, a template specialization of Kokkos::reduction_identity<CustomType> must be defined.  See below for an example.
 * [Kokkos::Sum](Kokkos%3A%3ASum)

 * ```c++
   template<class Scalar, class Space>
   class Prod;
   ```
   Uses the multiply operation to combine partial results.
   * `Prod<T,S>::value_type` is `T`
   * `Prod<T,S>::result_view_type` is `Kokkos::View<T,S,Kokkos::MemoryTraits<Kokkos::Unmanaged>>`
   * Requires: `Scalar` has `operator =` and `operator *=` defined. `Kokkos::reduction_identity<Scalar>::prod()` is a valid expression. 

 * ```c++
   template<class Scalar, class Space>
   class Min;
   ```
   Selects the minimum value from combined inputs.
   * `Min<T,S>::value_type` is `T`
   * `Min<T,S>::result_view_type` is `Kokkos::View<T,S,Kokkos::MemoryTraits<Kokkos::Unmanaged>>`
   * Requires: `Scalar` has `operator =` and `operator <` defined. `Kokkos::reduction_identity<Scalar>::min()` is a valid expression. 

 * ```c++
   template<class Scalar, class Space>
   class Max;
   ```
   Selects the minimum value from combined inputs.
   * `Max<T,S>::value_type` is `T`
   * `Max<T,S>::result_view_type` is `Kokkos::View<T,S,Kokkos::MemoryTraits<Kokkos::Unmanaged>>`
   * Requires: `Scalar` has `operator =` and `operator >` defined. `Kokkos::reduction_identity<Scalar>::max()` is a valid expression. 

 * ```c++
   template<class Scalar, class Space>
   class LAnd;
   ```
   Uses the logical 'and' operation to combine partial results.
   * `Land<T,S>::value_type` is `T`
   * `Land<T,S>::result_view_type` is `Kokkos::View<T,S,Kokkos::MemoryTraits<Kokkos::Unmanaged>>`
   * Requires: `Scalar` has `operator =` and `operator &&` defined. `Kokkos::reduction_identity<Scalar>::land()` is a valid expression. 

 * ```c++
   template<class Scalar, class Space>
   class LOr;
   ```
   Uses the logical 'or' operation to combine partial results.
   * `LOr<T,S>::value_type` is `T`
   * `LOr<T,S>::result_view_type` is `Kokkos::View<T,S,Kokkos::MemoryTraits<Kokkos::Unmanaged>>`
   * Requires: `Scalar` has `operator =` and `operator ||` defined. `Kokkos::reduction_identity<Scalar>::lor()` is a valid expression. 

 * ```c++
   template<class Scalar, class Space>
   class BAnd;
   ```
   Uses the bitwise 'and' operation to combine partial results.
   * `BAnd<T,S>::value_type` is `T`
   * `BAnd<T,S>::result_view_type` is `Kokkos::View<T,S,Kokkos::MemoryTraits<Kokkos::Unmanaged>>`
   * Requires: `Scalar` has `operator =` and `operator &` defined. `Kokkos::reduction_identity<Scalar>::band()` is a valid expression. 

 * ```c++
   template<class Scalar, class Space>
   class Bor;
   ```
   Uses the bitwise 'or' operation to combine partial results.
   * `BOr<T,S>::value_type` is `T`
   * `BOr<T,S>::result_view_type` is `Kokkos::View<T,S,Kokkos::MemoryTraits<Kokkos::Unmanaged>>`
   * Requires: `Scalar` has `operator =` and `operator |` defined. `Kokkos::reduction_identity<Scalar>::bor()` is a valid expression. 

## Examples

  ```c++
    #include<Kokkos_Core.hpp>
    
    int main(int argc, char* argv[]) {

      long N = argc>1 ? atoi(argv[1]):100; 
      long result;
      Kokkos::parallel_reduce("ReduceSum: ", N, KOKKOS_LAMBDA (const int i, long& lval) {
        lval += i;
      },Sum<long>(result));

      printf("Result: %l Expected: %l\n",result,N*(N-1)/2);
    }
  ```

