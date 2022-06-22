# Sorting

ArrayList<Integer> arr = new ArryList<>();

* `Collections.sort(arr);` -> will sort arr in ascending order
* `Collections.sort(arr, Comparator.reverseOrder())` -> sort in descending order
* `Collections.sort(arr, Comparator.comparing(key_extractor))` -> first it will apply the key_extractor on all elements 
  to get a collection of comparable elements then it will apply simple sort on it.
* `Collections.sort(arr, (f,s) -> {...})` -> will sort the list according to the function


