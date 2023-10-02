# smart-contract-array
//ArrayUtils Library:
This library will offer two functions: one for sorting and another for removing duplicates from a uint array.
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

library ArrayUtils {

    // Simple bubble sort
    function sort(uint[] storage arr) internal {
        uint n = arr.length;
        for (uint i = 0; i < n-1; i++) {
            for (uint j = 0; j < n-i-1; j++) {
                if (arr[j] > arr[j+1]) {
                    (arr[j], arr[j+1]) = (arr[j+1], arr[j]);
                }
            }
        }
    }
    
    function removeDuplicates(uint[] storage arr) internal {
        sort(arr);
        
        if (arr.length == 0) return;

        uint[] memory temp = new uint[](arr.length);
        uint j = 0;

        for (uint i = 0; i < arr.length - 1; i++) {
            if (arr[i] != arr[i+1]) {
                temp[j++] = arr[i];
            }
        }
        temp[j++] = arr[arr.length - 1];

        for (uint i = 0; i < j; i++) {
            arr[i] = temp[i];
        }
        for (uint i = j; i < arr.length; i++) {
            arr.pop();
        }
    }
}
